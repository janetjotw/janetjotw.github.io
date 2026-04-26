---
title: "XML with Attributes"
date: 2019-03-20T10:30:20+00:00
draft: false
---

**You will learn how to write XML documentation when attributes exist**

Element | Attribute | Description | Type | Required | Notes |
| ---- | --- | --- | --- | --- | --- |
| recordTV | Top level | TV program data | data| Required |  |
| &nbsp;&nbsp;when |  | The date and time of the program | | Required |  |
| | &nbsp;&nbsp;date | The date of the program | string | Optional | the date format is YYYY-MM-DD; default is today's date |
| | &nbsp;&nbsp;time |The time of the program | string | Required | For 12-hr format HH:MM followed by am or pm |
| | &nbsp;&nbsp;format | The format for the time; either 12 or 24-hr| string | Required | 24 or 12 |
| duration | hours | duration of the program | number | Required | in hours |
| station | channel | channel to record | number | Required |    |

**You will learn how to write XML documentation when attributes exist**

Element
Attribute
Description
Type
Required
Notes

recordTV
Top level
TV program data
data
Required

  when

The date and time of the program

Required

  date
The date of the program
string
Optional
the date format YYYY-MM-DD; default is today’s date

  time
The time of the program
string
Required
For 12-hr format HH: MM followed by am or pm

  format
The format for the time; either 12 or 24-hr
string
Required
24 or 12

duration
hours
duration of the program
number
Required
in hours

station
channel
channel to record
number
Required