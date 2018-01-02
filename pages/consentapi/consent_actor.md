---
title: actor Element
keywords: actor, consent
tags: [profile,element,patient]
sidebar: overview_sidebar
permalink: consent_actor.html
summary: "low level details for the National Data Opt-out 'actor' element"
---

### Element Usage ###

actor uses the Consent.actor element to capture the patient or a healthcare professional who controls the consent. The value set will depend on how the consent was set e.g via NHS Choice or via GP Practice. 

### actor ###

|name|Data Type|Description|
| ------------- | ------------- | ------------- |
|actor| Reference | Backbone (parent) element to capture details about how consent is controlled.|
|role| CodeableConcept | The role the actor plays|
|reference| string | Resource that relates to the actor.|
|ActorPerson| Extension | Text string to capture a person e.g Mother, Son, Daughter, Carer, etc.|

Example of correct usage

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`role`| INF |Valid code taken from http://hl7.org/fhir/stu3/valueset-security-role-type. Fixed value.|
|![Tick](images/tick.png)|`reference`| https://directory.spineservices.nhs.uk/STU3/Practitioner/G9634669 |
|![Tick](images/tick.png)|`reference`| https://directory.spineservices.nhs.uk/STU3/Organization/A83627 |
|![Tick](images/tick.png)|`reference`| https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104 |

Examples of incorrect usage

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`role`| GP| invalid code, not supported by NDOP.|
|![Cross](images/cross.png)|`reference`| G1231231 | Valid national code, but no url to locate it.


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




