---
title: Capability Statement
keywords: foundations, fhir
tags: [foundations,use_case,fhir]
sidebar: overview_sidebar
permalink: foundations_use_case_get_the_fhir_conformance_profile.html
summary: "Use case for getting the FHIR server's capability statement profile."
---

{% include important.html content="The capabilityStatement provided is based on the requirements for the National Data Opt-out API. How this is implemented is outside the scope of this guide" %}


### Requirements capabilityStatement

<script src="https://gist.github.com/IOPS-DEV/af36c2f3f03a2b0641af9961f46073ea.js"></script>

JSON example can be viewed [(here)](Examples/NDOP-CapabilityStatement-Example-1.json)

### Instance capabilityStatement

<script src="https://gist.github.com/IOPS-DEV/599b0e7d4e2d1ff4545aa66e7da72f6a.js"></script>

JSON example can be viewed [(here)](Examples/NDOP-CapabilityStatement-Example-2.json)

#### Request Headers ####

Client SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:nationaldataoptout:fhir:rest:read:metadata`|
| `Ssp-Authorization`  | This will carry the base64 encoded JSON web token required for audit - see [Cross Organisation Audit and Provenance](https://nhsconnect.github.io/FHIR-NOO-API/development_security_jwt.html) for details. |

An example capabilityStatement profile is available [here](https://nhsconnect.github.io/FHIR-NOO-API/Examples/NDOP-CapabilityStatement-Example-1.xml) - client systems should always use the CapabilityStatement profile retrieved from the server being used as the authoritative capability statement - the example link above is provided as an example for reference only.

