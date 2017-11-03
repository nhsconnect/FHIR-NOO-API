---
title: consentingParty Element
keywords: party, consent
tags: [profile,element,patient]
sidebar: overview_sidebar
permalink: consent_consenting_party.html
summary: "low level details for the National Data Opt-out 'consentingParty' element"
---
### Element Usage ###

consenting party uses the Consent.consentingParty element to capture the consenter. This would typically be the patient themselves.  

### consenting party ###

|name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
|consentingParty| Reference | Captures the details of the organization or person who has granted consent to share the data. |

Example of correct usage

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`consentingParty`|https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104 |

Examples of incorrect usage

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`consentingParty`| https://demographics.spineservices.nhs.uk/STU3/Patient/450-557-7104|

XML example

```xml
    <consentingParty>
    	<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104"/>
    </consentingParty>
```

JSON example

```json
{
  "consentingParty": [
	{
     "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104"
  }
 ]
}
```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.



