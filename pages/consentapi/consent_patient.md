---
title: patient Element
keywords: patient, consent
tags: [profile,element,patient]
sidebar: overview_sidebar
permalink: consent_patient.html
summary: "low level details for the National Data Opt-out 'patient' element"
---
### Element Usage ###

patient uses the Consent.patient element to store a PDS reference that includes the patients 10 digit NHS number which has been allocated to the instance via a succesful PDS trace using the patient demographics service (PDS). 

### patient ###

|name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
|patient| Reference |url reference to the patients 10 digit NHS number|

Example of correct usage

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`patient`| https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104| A valid reference that includes the patients NHS number with no spaces|

Examples of incorrect usage

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`patient`| 450-557-7104|Incorrect format. Missing url and has Hyphens between digits|
|![Cross](images/cross.png)|`patient`| 4505577104|Incorrect format. Missing url.|

XML Example

```xml
    <patient>
    	<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104"/> 
    </patient>
```

```json
{
  "patient": [
	{
	  "reference" : "https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104""
	}
   ]
}
```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.





