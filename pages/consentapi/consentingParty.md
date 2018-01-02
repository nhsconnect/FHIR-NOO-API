---
title: consentingParty Element
keywords: consentingParty, consent
tags: [profile,element,patient]
sidebar: overview_sidebar
permalink: consentingParty.html
summary: "low level details for the National Data Opt-out 'consentingParty' element"
---

### Element Usage ###

consentingParty uses the Consent.consentingParty element to capture the patient who grants access rights to the National Data opt-out preferences. Where this element is populated, it MUST only be populated with a patient reference. Where the element is not populated, a consentingProxyRole MUST be populated. Only a patient or proxy can grant or revoke access.

### consentingParty ###

|name|Data Type|Description|
| ------------- | ------------- | ------------- |
|consentingParty| Reference | Contains a reference to the patient who grants the rights to access their National data Opt-out preferences.|


Example of correct usage

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`consentingParty`| https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104 |Literal reference to patient's PDS resource.

Examples of incorrect usage

|Usage| Element| examples| Comments|
|![Tick](images/cross.png)|`consentingParty`| https://demographics.spineservices.nhs.uk/STU3/Practitioner/G1231231 |A practitioner cannot grant access rights to a National data opt-out resource.


XML example

```xml
<actor>
  <role>
    <coding>
      <system value="http://hl7.org/fhir/v3/ParticipationType"/>
      <code value="INF"/> 
    </coding>
  </role>
  <reference>
    <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104"/>
  </reference>
</actor>
```

JSON example

```json
{
"actor": [
    {
      "role": {
        "coding": [
          {
            "system": "http://hl7.org/fhir/v3/ParticipationType",
            "code": "INF"
          }
        ]
      },
      "reference": {
        "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104"
      }
    }
  ]
}
```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.




