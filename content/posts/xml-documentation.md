---
title: "XML documentation"
date: 2019-03-20T10:11:35+00:00
draft: false
---

**You will learn how to approach XML documentation**

2015-06-01
18:00
1.5
54

Element | Description | Type | Required  | Notes |
| --- | --- | --- | --- | --- |
recordTV | Top level | TV program data | Required   |  |
&nbsp;&nbsp;date | The date of the program | string | Optional  | default will include today's date|
&nbsp;&nbsp;time | The time program begins | number | Required | **24 or 12-hour** format; if 12-hr then HH:MM followed by AM or PM format|
&nbsp;&nbsp;duration | The length of the program  | number | Required  | In hours |
&nbsp;&nbsp;channel | The date of the program  | number | Required |  if not included it will include today's date|

**You will learn how to write XML documentation**

 

2015-06-01 18:00 1.5 54

Element
Description
Type
Required
Notes

recordTV
Top level
TV program data
Required

  date
The date of the program
string
optional
the default will include today’s date

  time
The time program begins
number
Required
**24 or 12-hour** format; if 12-hr then HH: MM followed by AM or PM format

  duration
The length of the program
number
Required
In hours

  channel
The date of the program
number
Required
if not included it will include today’s date