---
title: Profile Elements
keywords: elements, consent
tags: [profile,elements,usage]
sidebar: overview_sidebar
permalink: development_elements.html
summary: "Implementation guide on the characteristics and usage of the profiles elements"
---

## Consent Profile Elements ##

|Name|Data Type|Card|Description|Value|
|----|---------|----|-----------|-----|
|[`id`](consent_id.html)|string|1..1|Logical id assigned by the FHIR server|Any UUID|
|[`status`](consent_status.html)|string|1..1|The current status of the consent instance|active,inactive|
|[`patient`](consent_patient.html)|Reference|1..1|Spine reference to the patients NHS number traced from PDS|
|[`dateTime`](consent_datetime.html)|dateTime|1..1|Date and time instance was last updated|Date+Time+TimeZone|
|[`actor`](consent_actor.html)|backbone|1..1|Captures the patient or healthcare professional who controls the consent|N/A|
|`actor.role`|CodeableConcept|1..1|Valueset for the role|INF=informant|
|`actor.reference`|Reference|1..1|URL for the actor|
|`actor.extension.actorperson`|String|0..1|Proxy for patient e.g Parent|Patients Mother|
|[`organization`](consent_organization.html)|Reference|1..1|Spine reference to the NHS Digital ODS code|MUST be a URL|
|[`policy`](consent_policy.html)|uri|1..1|Policy that the consent refers to|Should be able to resolve policy url|
|[`purpose`](consent_purpose.html)|Coding|1..1|Contains Opt-Out for Research or Commissioning & Planning|RESCH, PLAN|


## Consent Extensions ##

National Data Opt-out Source of Opt-Out extension

|Name|Data Type|Card|Description|
|----|---------|----|-----------|
|[`actor.actorperson`](consent_extension_actorperson.html)|extension|0..1|String value to capture person|Mother of patient|
|[`SourceOfOptOut`](consent_extension_sourceofoptout.html)|extension|1..1|Extension to capture the source that defined the national opt-out preferences e.g NHS Choice, GP System|




