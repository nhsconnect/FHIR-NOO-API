---
title: purpose Element
keywords: purpose, consent
tags: [profile,element,purpose]
sidebar: overview_sidebar
permalink: consent_purpose.html
summary: "low level details for the National Data Opt-out 'purpose' element"
---

### Element Usage ###

purpose uses the Consent.purpose element to set the Opt-out preferences that the patient has chosen. Valid codes are taken from the CodeSystem [https://snomed.info/sct](https://snomed.info/sct).

### status ###

|name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
|purpose|Coding| The code used to identify which national data opt-out has been enabled|


Example of correct usage

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`purpose`| 370856009|SNOMED CT code used to describe the consent purpose.  |

Examples of incorrect usage

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`purpose`| HRESCH|This code is taken from the default codesystem and is not supported.|


XML example

```xml
	<purpose>
		<system value="https://snomed.info/sct"/>
		<code value="370856009"/>
		<display value="Limiting access to confidential patient information"/>
	</purpose>
```

JSON example

```json
{
  "purpose": [
	{
    "system": "https://snomed.info/sct",
    "code": "370856009",
    "display": "Limiting access to confidential patient information"
  }
 ]
}
```
*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.




