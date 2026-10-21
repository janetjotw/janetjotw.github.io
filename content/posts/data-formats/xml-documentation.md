---
title: "XML documentation"
date: 2019-03-20T10:11:35+00:00
draft: false
---

**Learn XML documentation**

| Element | Description | Type | Required | Notes |
|---|---|---|---|---|
| `recordTV` | Top level | TV program data | Required | |
| `recordTV.date` | The date of the program | string | Optional | The default is today's date |
| `recordTV.time` | The time the program begins | number | Required | **24-hour** or **12-hour** format; for 12-hour, use `HH:MM` followed by `AM` or `PM` |
| `recordTV.duration` | The length of the program | number | Required | In hours |
| `recordTV.channel` | The date of the program | number | Required | If not included, it will include today's date |
