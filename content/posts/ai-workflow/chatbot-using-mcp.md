---
title: "AI Workflow: A Local Chatbot for API Docs using MCP and Qwen"
date: 2026-11-18
tags: ["AI workflow", "MCP", "Ollama", "Qwen", "API documentation", "Node.js"]
---

# AI Workflow: A Local Chatbot for API Docs Using MCP and Qwen

I built a command-line chatbot that answers developer questions about the Intellicheck IDN-Direct API. It connects to the API's published **Model Context Protocol (MCP) server** and lets a local LLM (**Qwen**, running in **Ollama**) call that server's tools to look up endpoints, request bodies, response schemas, and code samples.

The result is a docs assistant that answers from the source of truth, runs entirely on my laptop with a free local model, and works with any MCP server by changing one setting.

## The problem

Developers integrating with an API usually have the same questions:

- What endpoints exist, and which one do I need?
- What does the request body for this endpoint look like?
- What will the response contain?
- Can I see a working code example?

The answers already exist in the API reference documentation, but finding them means reading schemas. A general-purpose AI model can answer faster, but it doesn't know a specific API and tends to invent endpoints and parameters.


## Architecture

```
┌──────────┐   question   ┌──────────────────────┐   tool calls   ┌───────────────────────────┐
│Developer │ ───────────► │  Chatbot (Node.js)   │ ─────────────► │ IDN-Direct MCP server     │
│ (CLI)    │ ◄─────────── │  MCP client          │ ◄───────────── │ (ReadMe, OpenAPI tools)   │
└──────────┘    answer    │       ▲      │       │  tool results  └───────────────────────────┘
                          │       │      ▼       │
                          │  ┌────────────────┐  │
                          │  │ Qwen via Ollama│  │
                          │  │ (local LLM)    │  │
                          │  └────────────────┘  │
                          └──────────────────────┘
```

## How it works

The solution covers the steps for the AI assistant or the chatbot to connect a local LLM client to the MCP server to query the API schema and endpoints.

### Pre-requisites

| Setting | Default | Purpose |
| --- | --- | --- |
| `MCP_URL` | `https://idn-direct-api.readme.io/mcp` | MCP server to connect to |
| `LLM_PROVIDER` | `ollama` | `ollama` or `anthropic` | Runs models locally, free, no data leaves the laptop; Use `qwen3:8b` |
| `OLLAMA_MODEL` | (set to your model) | Local model, for example `qwen3:8b` |
| `ANTHROPIC_API_KEY` | (none) | Required only for Claude |
| `MAX_TOOL_ROUNDS` | `6` | Tool-call rounds allowed per question |

## MCP Tools

The Intellicheck Direct Developer Hub (hosted on ReadMe) publishes an MCP server at `https://idn-direct-api.readme.io/mcp`. MCP is an open protocol that lets AI applications discover and call *tools* that a server exposes. This server exposes tools generated from the API's OpenAPI specification:

| Tool | What it does |
| --- | --- |
| `list-endpoints` | Lists all API endpoints |
| `get-endpoint` | Returns details for one endpoint |
| `get-request-body` | Returns an endpoint's request parameters |
| `get-response-schema` | Describes an endpoint's response structure |
| `search-schema` | Searches the API specification |
| `get-code-snippet` | Returns a code example in a chosen language |
| `execute-request` | Calls the (simulated) API |

My chatbot is an **MCP client**. It connects to the server, discovers these tools, hands them to the LLM, and runs the tool calls the model asks for.


## Design decisions

- **Tools are discovered, not hard-coded** The chatbot reads the tool list from the server at startup. If the server adds tools, the chatbot uses them without code changes, and pointing `MCP_URL` at a different server turns it into an assistant for a different API.
- **Provider-agnostic** The tool loop is written once per provider (Ollama and Anthropic) behind the same interface. Switching from a local model to Claude is a matter of setting `LLM_PROVIDER=anthropic`.
- **Grounded answers** The system prompt tells the model to base answers on tool results and to say when the tools don't have the information.
- **Guardrails for small models** A maximum number of tool rounds per question prevents loops, and large tool results are truncated to fit smaller context windows.
- **Honest about simulated data.** The IDN-Direct API on this server is simulated, so the prompt reminds the model that `execute-request` results are close to, but not exactly, production behavior.


## Running it

```bash
npm install
ollama pull qwen3:8b
OLLAMA_MODEL=qwen3:8b npm start
```

### How a question is answered

1. **Connect and discover.** On startup, the chatbot connects to the MCP server (Streamable HTTP, with SSE as a fallback) and calls `listTools` to get each tool's name, description, and input schema.
2. **Offer the tools to the model.** It converts the MCP tool definitions into the function-calling format Ollama expects and sends them with the user's question and a system prompt.
3. **Run the tool loop.** If Qwen responds with tool calls, the chatbot executes each one against the MCP server and returns the results to the model. This repeats (up to a set limit) until the model has what it needs.
4. **Answer.** Qwen writes the final answer based on the tool results.

Every tool call is printed in the terminal, so the user can see exactly where an answer came from:

```
You: How do I create a valid /start request?
   get-request-body({"path":"/start","method":"post"})

Assistant: ...
```

## What I learned

- **Model size matters for tool use.** I started with IBM's `granite3.3:2b`. It runs well for chat, but small models are inconsistent at choosing tools and building arguments. Moving to Qwen made tool selection noticeably more reliable.
- **Chat models and embedding models do different jobs.** In an earlier RAG experiment, the same small chat model failed when asked to create embeddings. Retrieval needs an embedding model; answering needs a chat model. MCP sidesteps this for API reference because the server's tools do the lookup.
- **MCP turns documentation into an interface.** The quality of the answers depends on the quality of the API spec behind the tools: clear operation summaries, parameter descriptions, and examples. That's documentation work.

## Limitations and next steps

**The chatbot only covers the API reference.** The IDN-Direct MCP server exposes OpenAPI tools, so the chatbot can't answer questions about the hub's guides (setup, demo accounts, workflows). There are two ways to close that gap:

1. **Enable documentation tools on the platform.** ReadMe can add `search` and `fetch` tools to the same MCP server, giving the AI full-text search across the guides. Because my chatbot discovers tools at startup, it would use them without code changes. The `search`/`fetch` pair also follows the interface OpenAI defined for ChatGPT deep research, so the same server works with ChatGPT, Claude, Cursor, and other MCP clients.
2. **Build a docs MCP server.** Index the guides (via `llms.txt` or a crawl) into a vector store, expose `search_docs` and `get_page` tools, and let the chatbot connect to both the API server and the docs server at once.

Other next steps:

- Support multiple MCP servers in one session.
- Show source links for every answer.
- Add a web UI so the assistant can sit on a docs site.

## References

- [Intellicheck Direct Developer Hub: MCP](https://idn-direct-api.readme.io/docs/mcp)
- [ReadMe: Your project's MCP server](https://docs.readme.com/docs/your-projects-mcp-server)
- [Model Context Protocol](https://modelcontextprotocol.io)
- [Ollama](https://ollama.com)
