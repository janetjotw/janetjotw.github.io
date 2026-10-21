---
title: "JSON: 3-day weather forecast"
date: 2019-03-20T09:53:46+00:00
draft: false
---

## Sample JSON for a three-day forecast

```json
{
  "longitude": 47.60,
  "latitude": 122.33,
  "forecasts": [
  {
  "date": "2015-09-01",
  "description": "sunny",
  "maxTemp": 22,
  "minTemp": 20,
  "windSpeed": 12,
  "danger": false
  },
  {
  "date": "2015-09-02",
  "description": "overcast",
  "maxTemp": 21,
  "minTemp": 17,
  "windSpeed": 15,
  "danger": false
  },
  {
  "date": "2015-09-03",
  "description": "raining",
  "maxTemp": 20,
  "minTemp": 18,
  "windSpeed": 13,
  "danger": false
  }
]
}
```

The forecasts array shows the weather for 3 days, and this is just a sample array. It can have n number of days.

| Element  |  Description | Type | Notes |
| ---  |  --- | --- | --- |
| longitude  |  Longitude of the location where the forecast takes place | number | |
| latitude  |  Latitude of the location where the forecast takes place | number | |
| forecast  |  Daily forecast | array of daily forecast objects | |
| &nbsp; &nbsp; date  |  Date of the forecast | string | Format is YYYY-MM-DD|
| &nbsp; &nbsp; description  |  Text description of the weather | string | Valid values: sunny, overcast, partly cloudy, raining, and snowing |
| &nbsp; &nbsp; maxTemp  |  High temperature | number | In degrees Celsius |
| &nbsp; &nbsp; minTemp  |  Low temperature | number | In degrees Celsius |
| &nbsp; &nbsp; windSpeed  |  Wind speed | number | In kilometers per hour |
| &nbsp; &nbsp; danger  |  true if the weather conditions are dangerous; otherwise, false. | Boolean | |

## Sample JSON for three-day forecast**

```json
{
  “longitude”: 47.60,
  “latitude”: 122.33,
  “forecasts”: [
  {
  “date”: “2015-09-01”,
  “description”: “sunny”,
  “maxTemp”: 22,
  “minTemp”: 20,
  “windSpeed”: 12,
  “danger”: false
  },
  {
  “date”: “2015-09-02”,
  “description”: “overcast”,
  “maxTemp”: 21,
  “minTemp”: 17,
  “windSpeed”: 15,
  “danger”: false
  },
  {
  “date”: “2015-09-03”,
  “description”: “raining”,
  “maxTemp”: 20,
  “minTemp”: 18,
  “windSpeed”: 13,
  “danger”: false
  }
]
}

```

The forecasts array shows the weather for 3 days, and this is just a sample array. It can have n number of days.

The forecasts array shows the weather for 3 days, and this is just a sample array. It can have n number of days.

| Element | Description | Type | Notes |
|---|---|---|---|
| `longitude` | Longitude of the location where the forecast takes place | number | |
| `latitude` | Latitude of the location where the forecast takes place | number | |
| `forecast` | Daily forecast | array of daily forecast objects | |
| `forecast.date` | Date of the forecast | string | Format is YYYY-MM-DD |
| `forecast.description` | Text description of the weather | string | Valid values: `sunny`, `overcast`, `partly cloudy`, `raining`, and `snowing` |
| `forecast.maxTemp` | High temperature | number | In degrees Celsius |
| `forecast.minTemp` | Low temperature | number | In degrees Celsius |
| `forecast.windSpeed` | Wind speed | number | In kilometers per hour |
| `forecast.danger` | `true` if the weather conditions are dangerous; otherwise, `false` | Boolean |
