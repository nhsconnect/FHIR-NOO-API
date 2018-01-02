---
title: status Element
keywords: status, consent
tags: [profile,element,status]
sidebar: overview_sidebar
permalink: consent_status.html
summary: "low level details for the National Data Opt-out 'status' element"
---
### Element Usage ###

Consent uses the Consent.status element to indicate whether the patient has agreed to data sharing or has opted out of one or both types defined within the national data opt-out policy. When a patient indicates they wish to Opt-out of a data sharing agreement, one instance will be created per Opt-out, e.g Patient A opts out of research only creates one unique instance. Patient B Opts out of both research data and the commissioning data, creates two unique instances. When these instances are created the status for each instance will be set to 'active', indicating that the patient has an active opt-out in place. No data will be shared for that specific opt-out whilst the status is 'active'.

Should a patient who **has previously opted out of data sharing** decides to permit their data to be shared, the existing active instance or instances are retrieved and updated by the patient to indicate they now wish to share their data for research and/or commissioning. The status is then updated to 'inactive' for one or both instances depending on patient choice. The instances now permit data sharing to occur. 

{% include important.html content="Where a consent instance does not exist, it is implied that the patient has agreed to national opt-out data sharing." %}

### status ###

|Element Type| Data Type| Description|
| ------------- | ------------- | ------------- |
| code| string | The current status of the consent instance.|


- `active` is used to indicate that the patient has agreed to opt-out of national data sharing for specified purpose.
- `inactive` is used to indicate that the patient has agreed to data sharing for a specified purpose. 
- No other code is permitted to be used as a status of a consent instance.
- Where a patient updates one or both of their preferences, the status code will be updated accordingly.

Example of correct usage

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`status`| active|Patients data for research and/or planning and commissioning will **NOT** be shared|
|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`status`| inactive|Patients data for research and/or planning and commissioning will be shared|

Examples of incorrect usage

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`status`|proposed |Although status is a valid FHIR code, it is an invalid NDOP code.|

### Examples ###

XML Body

```xml
<status value="active"/>
```
JSON Body

```json
{
 "status": "active"
}
```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.








