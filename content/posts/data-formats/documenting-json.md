---
title: "Documenting JSON"
date: 2019-03-20T09:44:17+00:00
draft: false
---

## JSON structure to a Table
Come join me in learning how to document a JSON response. A sample JSON response is shown below. We will be learning to document the JSON response in a table.
```
{
"date": "2015-09-01",
"description": "sunny",
"maxTemp": 22,
"minTemp": 20,
"windSpeed": 12,
"danger": false
}
```
```
Element | Description | Type | Notes |
| --- | --- | --- | --- |
| date | The date of the forecast | String | YYYY-MM-DD format |
| description | The weather conditions| String | Values: sunny, raining, snowing, and partly cloudy.
| maxTemp | The maximum temperature of the day | number | temp in degree Celsius |
| minTemp | The minimum temperature of the day | number | temp in degree Celsius |
| windSpeed | The wind conditions| number | in kilometers per hour|
| danger | true if the weather conditions are dangerous; otherwise false | boolean | true or false|
```

**Sample JSON for 1-day forecast**
Here, we are learning how to document a JSON response. The sample JSON response is as below. We will document this response in a table.
```
{
“date”: “2015-09-01”,
“description”: “sunny”,
“maxTemp”: 22,
“minTemp”: 20,
“windSpeed”: 12,
“danger”: false
}
```

Element
Description
Type
Notes

date
The date of the forecast
String
YYYY-MM-DD format

description
The weather conditions
String
Values: sunny, raining, snowing, and partly cloudy.

maxTemp
The maximum temperature of the day
number
temp in degree Celsius

minTemp
The minimum temperature of the day
number
temp in degree Celsius

windSpeed
The wind conditions
number
in kilometers per hour

danger
true if the weather conditions are dangerous; otherwise false
boolean
true or false

Note: Thanks to Peter Greunbaum for these exercises.
