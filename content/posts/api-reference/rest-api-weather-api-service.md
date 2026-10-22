---
title: "REST API - Weather API Service"
date: 2026-10-21T10:50:40+00:00
draft: false
---

**Table of Contents**

- [Introduction](https://entwineinwords.wordpress.com/2019/02/27/rest-api-call-to-get-weather-and-wind-updates-from-a-weather-api-service/#introduction)
- [Overview of REST](https://entwineinwords.wordpress.com/2019/02/27/rest-api-call-to-get-weather-and-wind-updates-from-a-weather-api-service/#2-overview-of-rest)
- [Get weather conditions for a location](https://entwineinwords.wordpress.com/2019/02/27/rest-api-call-to-get-weather-and-wind-updates-from-a-weather-api-service/#3-get-weather-conditions-for-a-location)
- [Get wind conditions at a location](https://entwineinwords.wordpress.com/2019/02/27/rest-api-call-to-get-weather-and-wind-updates-from-a-weather-api-service/#4-get-wind-conditions-at-a-location)
- [Final output](https://entwineinwords.wordpress.com/2019/02/27/rest-api-call-to-get-weather-and-wind-updates-from-a-weather-api-service/#5-final-output)

## Introduction

This page documents a sample REST API call to get weather and wind updates from a Weather API Service.

Let's get started with the fundamentals of **API** and web services before we understand REST. You can learn how to invoke a REST API call to get the weather and wind conditions of a place.

**API** stands for **Application Programming Interface**. API is the connecting medium or interface between two systems. If you have registered with any social media account and try to login with your credentials, there is an API call that checks to verify if you are a registered user.

APIs are similar to Web services. Web services are web-based applications that help in communication exchange between a client and a server. The client, user or a program, requests a resource and the server responds to the request by returning a response. The requests are made through a web protocol called the Hypertext Transfer Protocol (HTTP) for a request-response mechanism.

**Representational State Transfer (REST)** uses HTTP as the protocol for the message request and response. REST APIs are called RESTFul APIs.

## Overview of REST

- REST APIs are different from its predecessor SOAP.

- An API is an interface between two systems, how they communicate and interact with each other.

- Web services use HTTP protocol for communicating a user request and to return a response.

- They are language agnostic and work on any platform for communication. You can code in a programming language--Java, NodeJs, Go, Python, etc.

- When a system makes a request, a response is generated.

The following diagram shows the request from a client when the URL is typed on the browser and the response is returned in either XML or JSON format.

![](/images/rest-api-weather-api-service/restarch.png)

Image source: [https://idratherbewriting.com/learnapidoc/docapis_what_is_a_rest_api.html](https://entwineinwords.wordpress.com/blog/)

## Get weather conditions for a location

This endpoint retrieves the weather conditions for a specified location.

```
`GET /weather`
```

**Authorization**

Sign up to get the API Key from the `openweathermap API` service. 

We will use the `appid` to authorize the OpenWeatherMap API to consume the service.

**Request**

```bash
`https://api.openweathermap.org/data/2.5/weather?zip=75098&units=imperial&appid=2ac115d3bf152bd58d446dcf3b07ea55`
```

**Input parameters **

API key (appid) and the zip code (zip) of the place.

API key is a secret code that you need beforehand.

**Curl Request**

```bash
`curl -X 'GET' \
  'https://api.openweathermap.org/data/2.5/weather?zip=75098&units=imperial&lang=en&mode=json&appid=2ac115d3bf152bd58d446dcf3b07ea55' \
  -H 'accept: application/json'`
```

Type the above curl script in your terminal and observe the response.

**Response**

The response returned is a JSON object or a payload with key-value pairs.

```json
{
  "coord": {
    "lon": -96.5394,
    "lat": 33.0041
  },
  "weather": [
    {
      "id": 800,
      "main": "Clear",
      "description": "clear sky",
      "icon": "01d"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 87.55,
    "feels_like": 94.64,
    "temp_min": 84.29,
    "temp_max": 91.09,
    "pressure": 1014,
    "humidity": 61
  },
  "visibility": 10000,
  "wind": {
    "speed": 8.05,
    "deg": 230
  },
  "clouds": {
    "all": 0
  },
  "dt": 1660661068,
  "sys": {
    "type": 2,
    "id": 2005310,
    "country": "US",
    "sunrise": 1660650604,
    "sunset": 1660698663
  },
  "timezone": -18000,
  "id": 0,
  "name": "Wylie",
  "cod": 200
}
```

**Note**: There are tools like [Postman ](https://www.getpostman.com/downloads/)or [Swagger](https://swagger.io/) that help with writing and validating the API calls. The Swagger online editor to write the OpenAPI specification document can be seen. 

![](/images/rest-api-weather-api-service/swaggerweather.png)

The screenshot shows a sample HTML file where the GET request is invoked to get the weather conditions.

![](/images/rest-api-weather-api-service/weatherapi.png)

## Get wind conditions at a location

This endpoint retrieves the wind conditions for the zip code and country code.

```
`GET /weather`
```

**Request**

```bash
`https://api.openweathermap.org/data/2.5/weather?zip=75098,us&appid=2ac115d3bf152bd58d446dcf3b07ea55&units=imperial`
```

**Input parameter**

API key, the zip code of the place, and the country code.

**Response**

```json
{
  "coord": {
    "lon": -99.2506,
    "lat": 31.2504
  },
  "weather": [
    {
      "id": 804,
      "main": "Clouds",
      "description": "overcast clouds",
      "icon": "04d"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 82.65,
    "feels_like": 86.04,
    "temp_min": 80.74,
    "temp_max": 82.65,
    "pressure": 1015,
    "humidity": 63,
    "sea_level": 1015,
    "grnd_level": 953
  },
  "visibility": 10000,
  "wind": {
    "speed": 9.24,
    "deg": 171,
    "gust": 11.72
  },
  "clouds": {
    "all": 100
  },
  "dt": 1660662790,
  "sys": {
    "type": 2,
    "id": 265416,
    "country": "US",
    "sunrise": 1660651405,
    "sunset": 1660699163
  },
  "timezone": -18000,
  "id": 4736286,
  "name": "Texas",
  "cod": 200
}
```

The screenshot shows a sample HTML file where the GET request is invoked to get the wind conditions.

![](/images/rest-api-weather-api-service/weatherapi.png)

## Final output

When you open the browser and run the HTML file, the page is loaded as follows:

The screenshot shows the UI elements to check for wind before the button click.

![](/images/rest-api-weather-api-service/windbefore.png)

The UI response after the button click.

![](/images/rest-api-weather-api-service/windafter.png)

This shows how we can make REST API calls to get the desired output. REST is easy to learn; it is not tied to a programming language and can run on any platform.
