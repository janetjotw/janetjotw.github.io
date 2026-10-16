---
title: "Creating a webhook receiver"
date: 2025-01-30T12:22:31+00:00
draft: false
---

This tutorial covers how to create a sample webhook receiver to receive payloads.

The use cases for configuring a webhook could be an IoT device sending location coordinates, device sensor readings, payment notifications for an e-commerce application, and more.

Follow the following steps to install Python, Flask, and ngrok to get your setup ready to receive webhook data.

## Install Python

Refer to [Python, Boto3, and AWS RDS]({{< relref "posts/python-boto3-and-aws-rds.md" >}}), where I show how to install Python and check the version installed. You need Python 3.

## Install Flask

Use the Python package manager `pip` to install Flask.

```bash
pip install flask
```

## Install ngrok

I have macOS. See the [ngrok downloads page](https://ngrok.com/downloads/windows) for your operating system.

```bash
brew install ngrok
```

## Start server

Open another tab in your terminal and run the following command:

```bash
ngrok http 5000
```

## Create a base application

Now that your setup is ready, you'll create a Python app and run it to start the server.

You can use any editor. I use VS Code. You could also use a command-line editor `nano` to create the file.

```bash
nano main.py
```

```python
from flask import Flask, request, Response
import json

app = Flask(__name__)
@app.route('/webhook2', methods=['POST'])
def respond2():
    print("Json received in post: " + json.dumps(request.json, indent=4))
    return Response(status=200)
```

The `respond2()` view function returns the response with the `status code=200`.

To run your application, you'll tell Flask where to find the application `main.py` file with the `FLASK_APP` environment variable:

```bash
export FLASK_APP=main.py
```

Run the application using the Flask `run` command.

```bash
python3 -m flask run
```
