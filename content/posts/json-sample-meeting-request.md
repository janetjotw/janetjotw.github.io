---
title: "JSON - Sample meeting request"
date: 2019-03-20T09:55:07+00:00
draft: false
---

**JSON request to create a new meeting.** The JSON looks as below:

{
"meeting" : {
"time": "2015-09-01 10:00",
"duration": 60,
"description": "2016 Strategic Planning Meeting",
"location": "Building 23, Room 206",
"reminder": 15,
"invitees": ["michael@example.com", "thelma@example.com",
"david@example.com", "leon@example.com"]
}
}
Element|Description|Type|Notes|Required|
|---|---|---|---|---|
|meeting| The meeting request object|object| | Required|
|&nbsp;&nbsp;time| The meeting start time|String| GMT format| Required |
|&nbsp;&nbsp;duration| The duration of the meeting|number|in minutes | Required|
|&nbsp;&nbsp;desc| The meeting highlights|String| |Required |
|&nbsp;&nbsp;location| The meeting location|number|default is an empty string | optional|
|&nbsp;&nbsp;reminder| The meeting reminder|number|default is 10 mins | optional|
|&nbsp;&nbsp;invitees| The meeting invitee list|array of string| valid email address and default is empty array.| optional|

**JSON request to create a new meeting.** The JSON looks as below:

{
“meeting” : {
“time”: “2015-09-01 10:00”,
“duration”: 60,
“description”: “2016 Strategic Planning Meeting”,
“location”: “Building 23, Room 206”,
“reminder”: 15,
“invitees”: [“michael@example.com”, ["thelma@example.com](mailto:%22thelma@example.com)",
["david@example.com](mailto:%22david@example.com)", ["leon@example.com](mailto:%22leon@example.com)"]
}
}

Element
Description
Type
Notes
Required

meeting
The meeting request object
object

Required

  time
The meeting start time
String
GMT format
Required

  duration
The duration of the meeting
number
in minutes
Required

  desc
The meeting highlights
String

Required

  location
The meeting location
number
default is an empty string
optional

  reminder
The meeting reminder
number
default is 10 mins
optional

  invitees
The meeting invitee list
array of string
valid email address and default is empty array.
optional