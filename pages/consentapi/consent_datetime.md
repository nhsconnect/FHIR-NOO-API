---
title: dateTime Element
keywords: date, time
tags: [date,time]
sidebar: profiles_sidebar
permalink: consent_datetime.html
summary: "low level details for the National Data Opt-out 'dateTime' element"
---

### dateTime ###

|Data Type|Description|
| ------------- | -------------|
|dateTime |The date and time of day when the instance was last updated|


**Example of Correct Usage**

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`dateTime`| 1957-01-01T08:39:16+00:00|Correct format for a time stamp, comprising of date, time (including seconds) and a timezone|
|![Tick](images/tick.png)|`dateTime`| 1988-11-11T11:45+00:00|Correct format for a time stamp, comprising of date, time with seconds zero filled, and a timezone|

**Example of Incorrect Usage**

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)||1973-04-01|The time is not present.|
|![Cross](images/cross.png)||1987-01-23T24:00:00+00:00|The time 24:00 is not a valid time|
|![Cross](images/cross.png)||1987/01/23T21:33:00+00:00|The date separator uses / which is not valid|


On the wire XML example

```xml
<dateTime value="2017-02-01T11:15:33+00:00"/>
```

On the wire example in JSON

```json
{
"dateTime": "2016-01-02T08:39:16+00:00"
}
```

*Error Handling*

The provider system SHALL return an error if:

- `dateTime` is missing a time
- `dateTime` is missing a timezone
- `dateTime` date part is missing.







