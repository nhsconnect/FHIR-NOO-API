---
title: purpose Element
keywords: purpose, consent
tags: [profile,element,purpose]
sidebar: overview_sidebar
permalink: consent_purpose.html
summary: "low level details for the National Data Opt-out 'purpose' element"
---

### Element Usage ###

purpose uses the Consent.purpose element to set the Opt-out preferences that the patient has chosen. Valid codes are taken from the CodeSystem [https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1](https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1).

### status ###

|name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
|purpose|Coding| The code used to identify which national data opt-out has been enabled|


Example of correct usage

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`purpose`| RESCH|A consent record record exists for research and planning. |

Examples of incorrect usage

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`purpose`| HRESCH|This code is not valid when used with the https://fhir.nhs.uk/ValueSet/ndop-preferences-1 valueset|


XML example

```xml
    <purpose>
        <system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1"/>
        <code value="RESCH"/>
        <display value="healthcare research"/>
    </purpose>
```

JSON example

```json
{
  "purpose": [
	{
    "system": "https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1",
    "code": "RESCH",
    "display": "healthcare research"
  }
 ]
}
```
*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.




