---
title: "Creating a Webhook Receiver"
date: 2025-01-30T12:22:31+00:00
draft: false
---

This tutorial covers how to create a sample Webhook receiver to receive payloads.

The use cases for configuring a Webhook could be an IoT device sending location coordinates, device sensor readings, payment notifications for an e-commerce application, etc.

Follow the steps below to install Python, Flask, and ngrok to get your set up ready to receive Webhook data.

## Install Python

Refer to this [article](https://entwineinwords.wordpress.com/2022/08/13/python-boto3-and-aws-rds/) where I show how to install Python and check the version installed. You need Python3.

## Install Flask

Use the Python package manager `pip` to install Flask.

```
`pip install flask`
```

## Install ngrok

I have macOS. See the [ngrok](https://ngrok.com/downloads/windows) downloads page for your operating system.

```
`brew install ngrok`
```

## Start Server

Open another tab in your terminal and type the below command

```
`ngrok http 5000`
```

## Creating a Base application

Now that your setup is ready, you'll create a Python app and run it to start the server.

You can use any editor. I use VS Code. You could also use a command-line editor `nano` to create the file.

```
`nano main.py`
```

```
`from flask import Flask, request, Response
import json

app = Flask(_name_)
@app.route('/webhook2', methods=['POST'])
def respond2():
print("Json received in post: " + json.dumps(request.json, indent = 4))
return Response(status=200)`
```

The `respond2()` view function returns the response with the `status code=200`.

To run your application, you’ll tell Flask where to find the application main`.py` file with the `FLASK_APP` environment variable:

```
`export FLASK_APP=main.py`
```

Run the application using the Flask `run` command.

```
`python3 -m flask run`
```