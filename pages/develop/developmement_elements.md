---
title: Profile Elements
keywords: elements, consent
tags: [profile,elements,usage]
sidebar: overview_sidebar
permalink: development_elements.html
summary: "Implementation guide on the characteristics and usage of the profiles elements"
---
{% include custom/search.warnbanner.html %}

{% include custom/fhir.reference.html resource="Consent" page="NDOP-Consent-1" fhirlink="[Consent](https://www.hl7.org/fhir/consent.html)" content="N/A" userlink="" %}

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
|[`patient`](consent_patient.html)|Reference|1..1|Spine reference to the patients NHS number traced from PDS|
|[`status`](consent_status.html)|string|1..1|The current status of the consent instance|active,inactive|
|[`policy`](consent_policy.html)|uri|1..1|Policy which the Consent record relates to.|

## Consent Extensions ##

National Data Opt-out Source of Opt-Out extension

|Name|Data Type|Card|Description|
|----|---------|----|-----------|
|[`consentingProxyRole`](consent_extension_consentingproxyrole.html)|extension|0..1|Extension to capture proxy role e.g GUARDIAN|
|[`SourceOfOptOut`](consent_extension_sourceofoptout.html)|extension|1..1|Extension to capture the source that defined the national opt-out preferences e.g NHS Choice, GP System|
|[`NICReference`](consent_extension_nicreference.html)|extension|0..1|Extension to capture the National Information Centre (NIC) record reference where preference is set via the contact centre|

{% include custom/search.nopat.patient.html para="2.1.2." resource="Consent" content="patient"  example="https://demographics.spineservices.nhs.uk/STU3/Patient/6101231223" text1="patient" text2="6101231223" %}

{% include custom/get.consent.policy.html para="2.1.3." resource="Consent" content="patient and policy" text1="https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104" text2="NDOP-policy-Example-V1.0.pdf" %}


