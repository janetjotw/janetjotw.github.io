---
title: "Webhooks"
date: 2022-08-11T23:28:13+00:00
draft: false
---

- [History of web communication](https://entwineinwords.wordpress.com/2022/08/11/webhooks/#history-of-web-communication)- [Introduction to webhooks](https://entwineinwords.wordpress.com/2022/08/11/webhooks/#introduction-to-webhooks)- [What is a webhook?](https://entwineinwords.wordpress.com/2022/08/11/webhooks/#what-is-a-webhook)- [Why a webhook?](https://entwineinwords.wordpress.com/2022/08/11/webhooks/#why-a-webhook)- [Security](https://entwineinwords.wordpress.com/2022/08/11/webhooks/#security)- [Use cases](https://entwineinwords.wordpress.com/2022/08/11/webhooks/#use-cases)- [Example webhook payload](https://entwineinwords.wordpress.com/2022/08/11/webhooks/#example-webhook-payload)

Solution providers or enterprises today exhibit their available services or interfaces for the product offerings through APIs. Customers, developers, or third-party integrators can benefit from businesses exposing APIs by utilizing their solution through one of the integration mechanisms called webhooks.

Before you understand webhooks, have you ever wondered about the history of web communication or how two systems communicate with each other?

## History of web communication

A few different types of design architectures for information exchange for distributed systems exist. An underlying concept of web communication on how data is requested and a response is sent back is the request-response mechanism. This article will briefly explain the design patterns for data communication before we dive into webhooks.

**Publish/Subscribe**

The Publish/Subscribe pattern is also called Pub/Sub. Messages are transmitted out by the publisher (host) to the channel, which is also called a message broker and the subscriber receives the published message that it subscribed. Publishers push messages on a topic to the broker and the broker sends the message to the subscriber that subscribed to that topic. The broker acts like a middle man to route messages. 

There is a drawback to the pub/sub design due to the coupling around the message topic and structure. If the message structure changes, the subscriber must change the receiving structure else it leads to errors. Real-world examples include social media, IoT messages from a device that uses MQTT (MQ Telemetry Transport) protocol, AWS SNS.

![Pub/Sub diagram](/images/webhooks/pub-sub.png)

**Push/Pull**

**Push** - is a pattern where the server pushes the data to the client when the information is available. Examples of the push concept include notifications like an email or a webhook.

**Pull** is a technique where the client requests data from the server. The client can be a worker in a container requesting work from the server when it is ready to process the load. The client has to **poll or pull** messages from the queue. Examples include AWS SQS. Messages can't be received by multiple clients at the same time. Any one client can receive a message, process and delete it. Other receivers do not receive the same message later. Polling inherently introduces some latency in message delivery, unlike pub/sub where messages are immediately pushed to subscribers.

**Long Polling**

Long polling is a technique where the server keeps the incoming client connection open for as long as possible, delivering a response when it is available to the client. Long polling is server-side dependent. The traditional approach of the client requesting for data from the server remains the same, but the server may not respond immediately as it may have none. It responds when the data becomes available. There are pros and cons with long polling that includes performance and scaling. You can visualize an example of an email app sending requests to the server to check if a new mail has arrived.

![Long polling diagram](/images/webhooks/longpolling.png)

**WebSockets** 

WebSockets enable two-way real-time or bi-directional communication between two systems. Web Sockets keep the connection open for both the client and the server to exchange information. Examples include online games and chat.

To read more on webhooks and the tools that are supported, check out the [WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API).

There are quite a few out there that I haven't discussed. Leave a comment if you know more.

![WebSockets diagram](/images/webhooks/websockets.png)

Now that you understand some common web communication design patterns, let us dive into webhooks.

## **Introduction to webhooks**

## What is a webhook?

A push-based design is more effective than a poll--lesser strain on the network and resources. Webhook is a push-based design approach to publish data into third-party systems, near real time. It is a one-way communication system i.e., sending data from the system hosting the service to another system that would receive the data, and if needed act upon it. The system pushes data to the configured secured URL or an endpoint when an event is triggered. The receiver must be configured to adhere to the design structure of the incoming data. Webhook requests are sent as a `HTTP POST` method.

The diagram depicts a high-level overview of how a webhook interacts between two systems. When there is an event triggered on System A, which may be hosted on the Cloud or on-premises, a webhook push event sends the data or a payload to System B.

![Webhook diagram](/images/webhooks/webhook.png)

For System B to receive data on its endpoint, it must configure the URL of System B on System A and structure the incoming data based on the payload System A sends and may choose to write its application to process the information. It functions similar to Web service contracts. The payload can be in the format of JSON or an XML.

## Why a webhook?

Now you understand how a webhook functions and how it differs from polling. There is no need for the client to continuously poll the server for any new data. There is no exhaustion of resources on the client and the server and above all connections are not kept open for a long time. The connection is closed once the data is sent.

## Security

Make sure that when you offer webhook services, they are secure and follow some best practices in the industry. As discussed earlier, webhook data is sent on a `HTTP POST` request. However, to make it secure when you configure a webhook URL, the receiver could also configure an API Key so that the webhook sender can send the key in the HTTP header so that the receiver knows the incoming information is valid.

## Use cases

- You host an online boutique on eBay, and you want to be notified when an online payment happens for a purchase.

- Git commits on a repository--notify.

- IoT device sensor events.

## Example webhook payload

This is a sample webhook payload for an online payment.

```
`{
  "_id": "3434ccdfdfdfdfxxxx",
  "product_id": "acxxxxxxxx",
  "product_name": "Parka",
  "created_at": "2022-11-2T17:26:16.808603647Z",
  "customer": {
    "customer_id": "3434sssssssxx",
    "customer_name": "XYZ",
    "payment": {
      "invoice_id": "86868sdsdsdd",
       "updated_at": "2022-12-29T12:23:19.53Z"
     }
  }
}`
```
