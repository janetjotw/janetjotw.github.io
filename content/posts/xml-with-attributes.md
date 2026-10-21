---
title: "XML with Attributes"
date: 2019-03-20T10:30:20+00:00
draft: false
---

**Learn how to write XML documentation when attributes exist**

| Element | Attribute | Description | Type | Required | Notes |
|---|---|---|---|---|---|
| `recordTV` | | The TV program to record (top-level element) | element | Required | |
| &nbsp;&nbsp;`when` | | The date and time of the program | element | Required | |
| | `date` | The date of the program | string | Optional | Format is YYYY-MM-DD; default is today's date |
| | `time` | The start time of the program | string | Required | Format is HH:MM; for 12-hour time, add `am` or `pm` |
| | `format` | The time format | string | Required | Valid values: `12` or `24` |
| &nbsp;&nbsp;`duration` | `hours` | The length of the program | number | Required | In hours |
| &nbsp;&nbsp;`station` | `channel` | The channel to record | number | Required | |
