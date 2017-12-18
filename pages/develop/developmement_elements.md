---
title: Profile Elements
keywords: elements, consent
tags: [profile,elements,usage]
sidebar: overview_sidebar
permalink: development_elements.html
summary: "Implementation guide on the characteristics and usage of the profiles elements"
---
{% include custom/search.warnbanner.html %}

{% include custom/fhir.reference.html resource="Consent" page="NDOP-Consent-1" fhirlink="[Consent](https://www.hl7.org/fhir/consent.html)" content="User Stories" userlink="" %}

## 1. Read ##

<div markdown="span" class="alert alert-success" role="alert">
GET [baseUrl]/Consent/[id]</div>

{% include custom/read.response.html resource="Consent" content="" %}

## 2. Search ##

<div markdown="span" class="alert alert-success" role="alert">
GET [baseUrl]/Consent?[searchParameters]</div>

Fetches a bundle of all `Consent` resources for the specified search criteria.

{% include custom/search.header.html resource="Organization" %}

### 2.1. Search Parameters ###

{% include custom/search.parameters.html resource="Consent" link="https://www.hl7.org/fhir/consent.html#search)" %}


|Name|Data Type|Card|Description|Value|
|----|---------|----|-----------|-----|
|[`id`](consent_id.html)|string|1..1|Logical id assigned by the FHIR server|Any UUID|
|[`identifier`](identifier.html)|identifier|0..1|OPTIONAL consent identifier|An alternative method for identifying a resource|
|[`category`](category.html)|CodeableConcept|0..1|OPTIONAL category|MAY be used to categorise future Opt-outs|
|[`status`](consent_status.html)|string|1..1|The current status of the consent instance|active,inactive|
|[`patient`](consent_patient.html)|Reference|1..1|Spine reference to the patients NHS number traced from PDS|
|[`dateTime`](consent_datetime.html)|dateTime|1..1|Date and time instance was last updated|Date+Time+TimeZone|
|[`consentingParty`](consent_consentingParty.html)|reference|0..1|Use where patient is the consenting party.|MUST be a patient URL|
|[`organization`](consent_organization.html)|Reference|1..1|Spine reference to the NHS Digital ODS code|MUST be a URL|
|[`policy`](consent_policy.html)|uri|1..1|Policy that the consent refers to|Should be able to resolve policy url|
|[`purpose`](consent_purpose.html)|Coding|1..1|Contains Opt-Out purpose defined using SNOMED CT|370856009|

## Consent Extensions ##

National Data Opt-out Source of Opt-Out extension

|Name|Data Type|Card|Description|
|----|---------|----|-----------|
|[`consentingProxyRole`](consent_extension_consetingproxyrole.html)|extension|0..1|Complex extension to capture proxy role and an optional NIC reference e.g GUARDIAN / 1234ABC|
|[`SourceOfOptOut`](consent_extension_sourceofoptout.html)|extension|1..1|Extension to capture the source that defined the national opt-out preferences e.g NHS Choice, GP System|


{% include custom/search.nopat.patient.html para="2.1.1." resource="Consent" content="patient"  example="https://demographics.spineservices.nhs.uk/STU3/Patient/6101231223" text1="patient" text2="6101231223" %}
