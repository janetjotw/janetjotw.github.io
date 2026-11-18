---
title: "How to get IBM's Markdown RAG Assistant Running Locally"
date: 2026-11-18
tags: ["how-to", "RAG", "LangChain.js", "Ollama", "AI workflow"]
---

# RAG Assistant using Ollama

This how-to covers how to build a simple working example of retrieval-augmented generation (RAG) using Ollama. Ollama is a local platform for running open-weight models on your own hardware. This tutorial references the IBM Developer's tutorial, [Build a RAG-powered Markdown documentation assistant](https://developer.ibm.com/tutorials/build-rag-assistant-md-documentation/).

It runs entirely on your laptop, and it uses a real Markdown file as its knowledge source. This article walks through the setup and covers the three problems I hit, so you can get it running in one sitting instead of three.

## What you'll build

A command-line assistant that:

1. Downloads a Markdown file from a URL you give it.
2. Splits the file into chunks and stores them in an in-memory vector store.
3. Answers your questions about the file using a local model running in Ollama.

I tested it against one of my own posts, [Creating a Webhook Receiver](https://raw.githubusercontent.com/janetjotw/janetjotw.github.io/refs/heads/main/content/posts/how-to/creating-a-webhook-receiver.md), on a MacBook Pro.

## Before you start

You need:

- **Node.js 20.** The tutorial targets Node 18–20. If you already run a newer version, don't uninstall it. Use [nvm](https://github.com/nvm-sh/nvm) to run Node 20 for this project only (Step 1).
- **Ollama**, installed and running. On a Mac, the Ollama app starts the server for you.
- **The tutorial's project files.** Download `markdown-rag-tutorial-demo-main.zip` from the tutorial page.
- **A raw Markdown URL** to test with. On GitHub, open any `.md` file and click **Raw**.

## Step 1: Switch to Node 20

I was on Node 24. Rather than find out the hard way which dependency would object, I matched the version the tutorial was written for:

```bash
nvm install 20
nvm use 20
node -v
```

You should see `v20.x`. 

## Step 2: Pull the models

The tutorial uses one model. You need two, and Step 5 explains why.

```bash
ollama pull granite3.3:2b
ollama pull granite-embedding:30m
```

The tutorial also tells you to run `ollama serve`. If you get this error, you can ignore it:

```
Error: listen tcp 127.0.0.1:11434: bind: address already in use
```

It means Ollama is already running, usually because the desktop app started it. Run `ollama list` to confirm, then move on.

## Step 3: Unzip the project

```bash
unzip markdown-rag-tutorial-demo-main.zip
cd markdown-rag-tutorial-demo-main
ls
```

Make sure you can see `package.json` and `index.js` before you continue. Running `npm install` one folder too high is an easy mistake to make, and the error it gives you doesn't point you here.

## Step 4: Fix the dependencies, then install

This is where I lost the most time. My first `npm install` failed with:

```
npm error code ERESOLVE
npm error ERESOLVE unable to resolve dependency tree
...
npm error Found: @langchain/core@0.3.80
...
npm error peer @langchain/core@"^1.1.38" from @langchain/community@1.1.29
```

Read it slowly and it tells you exactly what's wrong. The project's `package.json` mixes two generations of LangChain. `@langchain/core` is pinned to the older 0.3 line, while `@langchain/community` and `@langchain/ollama` are on the newer 1.x line, which needs a newer core. npm can't satisfy both, so it stops.

Before choosing which way to go, I checked what the code actually imports:

```bash
grep -n "langchain" index.js
```

```
4:import { RecursiveCharacterTextSplitter } from "@langchain/textsplitters";
5:import { MemoryVectorStore } from "langchain/vectorstores/memory";
6:import { OllamaEmbeddings, ChatOllama } from "@langchain/ollama";
7:import { Document } from "@langchain/core/documents";
8:import { ChatPromptTemplate } from "@langchain/core/prompts";
```

Two useful things fall out of this. First, nothing imports `@langchain/community`, so it can go. Second, `MemoryVectorStore` comes from `langchain/vectorstores/memory`, an import path from the 0.3 line. So the right move is to bring everything *down* to 0.3, not up to 1.x.

You might expect `npm uninstall @langchain/community` to do the job. It doesn't: npm resolves the whole dependency tree even when you're removing something, so it fails on the next conflict instead. Edit `package.json` directly with `npm pkg`, which doesn't trigger resolution:

```bash
npm pkg delete dependencies.@langchain/community
npm pkg set dependencies.@langchain/core="^0.3.62"
npm pkg set dependencies.@langchain/ollama="^0.2.0"
npm pkg set dependencies.@langchain/textsplitters="^0.1.0"
npm pkg set dependencies.langchain="^0.3.0"
```

Then do a clean install:

```bash
rm -rf node_modules package-lock.json
npm install
```

You'll see a few `npm warn deprecated` lines and a note about vulnerabilities. For a local learning project, both are safe to ignore. The line that matters is `added ... packages`.

> **Don't reach for `--force` or `--legacy-peer-deps`.** Either flag gets the install to finish, but you end up with packages that don't fit together, and the errors move to runtime, where they're harder to read. Also, skip `npm audit fix --force`: it can quietly upgrade LangChain back to 1.x and put you right back at the start of this step.

## Step 5: Give embeddings their own model

With the install fixed, I ran the assistant, pasted in my URL, and got this far:

```
📥 Received markdown URL: https://raw.githubusercontent.com/...
🧩 Created 3 chunks
❌ Failed to create vector store: ResponseError: This server does not support embeddings. Start it with `--embeddings`
```

The download worked, and so did the chunking. The failure is at the embedding step, and the error message is misleading: there's no `--embeddings` flag to add to Ollama.

The real cause is that the tutorial uses `granite3.3:2b` for two different jobs. A **chat model** reads context and writes answers. An **embedding model** turns text into a list of numbers that represent its meaning, which is how the assistant finds the chunks relevant to your question. These are different kinds of models, and the chat model refused to do the embedding model's job.

The fix is to use the small embedding model you pulled in Step 2. Find where the code creates the embeddings:

```bash
grep -n -A3 "OllamaEmbeddings(" index.js
```

Change the model in that block to `granite-embedding:30m`:

```js
const embeddings = new OllamaEmbeddings({
  model: "granite-embedding:30m",
  // ...
});
```

Leave the `ChatOllama` model as `granite3.3:2b`. It still writes the answers.

## Step 6: Run it

```bash
node index.js
```

Paste a raw Markdown URL when prompted, wait for the chunks to be embedded, and ask a question about the file. This time, it answered.


*** IMPORTANT***:
>
- **Read the first error, not the last.** Both the npm and Ollama errors contained the answer. They just weren't phrased the way I wanted.
- **Check what the code imports before fixing dependencies.** One `grep` told me which package to delete and which version line to keep.
- **Embedding and chat models aren't interchangeable.** Real RAG setups use one of each. If you change embedding models later, re-embed your documents, because vectors from different models don't mix.

## Where this falls short

This tutorial is a great way to see RAG work end to end, but it's a demo, not a docs assistant. It reads one file per run and keeps its index in memory, so it re-embeds everything each time you start it and forgets it when you quit. Pointing it at a whole documentation site needs a persistent vector store, an indexer that only re-processes changed pages, and answers that cite their sources. That's the next thing I'm building.

## References

- IBM Developer: [Build a RAG-powered Markdown documentation assistant](https://developer.ibm.com/tutorials/build-rag-assistant-md-documentation/)
- [Ollama model library](https://ollama.com/library)
- [nvm (Node Version Manager)](https://github.com/nvm-sh/nvm)
