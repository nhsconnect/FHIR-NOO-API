---
title: id Element
keywords: id, consent
tags: [profile,element,id,design]
sidebar: overview_sidebar
permalink: consent_id.html
summary: "low level details for the care connect patient 'id' element"
---
{% include important.html content="The id element described is used to provide a unique method to identify a NHS patients consent preferences instance. This is not the patients NHS number, but a FHIR server generated UUID." %}

### Element Usage ###

National Data Opt-out uses the Consent.id element to store a universal unique identification (UUID) to each consent record that is created. Every new consent instance that is created using the National Data Opt-out service will be allocated a UUID to identify that record and will retain that UUID throughout the lifespan of the instance. Depending on the opt-out preferences set by the patient, they may have 1 or 2 instances. Where no preferences have been set by the patient, an instance will not exist.

{% include important.html content="The id is NOT required when a new instance is created (POST'd) on the FHIR server using REST. The id is used to retrieve or update a specific record." %}
### id ###

|Name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
|id| string | A unique logical identifier (UUID) allocated by the National Data Opt-out model.|

- 'id' **MUST** be used to uniquely identify a consent instance. This is the primary identifier for a patients consent preferences.

**Example of correct usage**

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`id`| 783ffeef-538e-4a17-bed2-983a382ccdd7 |Logical id stored as a string value.|

Examples of incorrect usage

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`id`| 402 556 1234|NHS number must not be used as the logical id| 


*Error Handling*

The provider system SHALL return an error if:

- the `id` is not a valid UUID
- the 'id' is missing









