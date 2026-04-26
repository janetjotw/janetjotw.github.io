---
title: "A sample Markdown file"
date: 2019-03-14T10:26:10+00:00
draft: false
---

This is my **Markdown page** and it’s great learning Markdown!

Lately, I have been using the **[Visual Studio Code](https://code.visualstudio.com/) (VS Code)** editor for generating Markdown files. VS Code is great for generating a pdf or an html file as your output. Markdown is a great tool for generating documents such as *Quick Start Guides*, *How-tos*, *Getting Started,* etc. to name a few.

A few of the things that I explored and learnt are:

 	- I used a combination of HTML and Markdown.
 	- HTML tags img for rendering images and resizing was more flexible than the markdown script.
 	- HTML tags for line breaks.
 	- Tabs for fenced code blocks ``` backticks before and after the code block.
For example:

 	Sample curl script for an API call

POST /gen/report
```
````bash
curl -X POST \

"https://test.io/api/v1/gen/report" \

-H "accept: application/json" \

-H "Authorization: xxxxxxxxxxxxx" \

-H "Content-Type: application/json" \

-d '{

xxxxxxxxxxx"

}'
`
```

 	- Sample JSON script

```
`
```json
{
"test":
    {
    "name: Janet,
    "site": entwineinwords.wordpress.com
    }
}
`
```

# Status Codes

Every HTTP request returns a response. The HTTP response returns a status code and a description. The codes indicates whether it was a success or an error. The common status codes are as below.

## Common codes

Code
Description

200
OK

403
Forbidden

404
Not found

Note: I have also used [https://stackedit.io/app#](https://stackedit.io/app#) online editor to produce Markdown files.