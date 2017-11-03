---
title: organization Element
keywords: orgnaization
tags: [profile,element,organization]
sidebar: profiles_sidebar
permalink: consent_organization.html
summary: "low level details for the National Data Opt-out 'organization' element"
---

### Element Usage ###

National Data Opt-out uses consent.organization to capture the custodian organization that manages the consent. This will be a fixed value of NHS Digital.

### organization ###

|Element Type| Data Type| Description|
| ------------- | ------------- | ------------- |
| code| url |The custodian organization|


Example of correct usage

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`organization`|https://directory.spineservices.nhs.uk/STU3/Organization/X26"|Organization should have a fixed value of 'X26' which is the ODS code for NHS Digital|

Examples of incorrect usage

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`organization`|NHS Choices |https://directory.spineservices.nhs.uk/STU3/Organization/E123123|Custodian cannot be a GP practice code|


On the wire XML example

XML example

```xml
    <organization>
    	<reference value="https://directory.spineservices.nhs.uk/STU3/Organization/X26"/>
    </organization>
```

JSON example

```json
{
  "organization": [
	{
      "reference": "https://directory.spineservices.nhs.uk/STU3/Organization/X26""
  }
 ]
}
```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.






