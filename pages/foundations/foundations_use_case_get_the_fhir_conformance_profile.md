---
title: Capability Statement
keywords: foundations, fhir
tags: [foundations,use_case,fhir]
sidebar: overview_sidebar
permalink: foundations_use_case_get_the_fhir_conformance_profile.html
summary: "Use case for getting the FHIR server's capability statement profile."
---

{% include important.html content="The capabilityStatement is out of scope for NDOP API. It is the responsibility of the service provider to establish a capabilityStatement for a FHIR endpoint that." %}


#### FHIR Capability Statement Request ####

The /metadata path on the root of the FHIR server will return the capability statement for the FHIR server:

```http
GET https://fhir.nhs.uk/metadata
```
- For details of this interaction - see the [HL7 FHIR specification](https://www.hl7.org/fhir/http.html#capabilities)
- Note: The mime-type can be specified to request either XML or JSON using another URL parameter `?_format=[mime-type]`, or a `Content-Type` HTTP header as per the [FHIR specification](https://www.hl7.org/fhir/http.html#mime-type).


#### Request Headers ####

Client SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `From`           | Consumer's ASID |
| `To`             | Provider's ASID |
| `InteractionID`  | `urn:nhs:names:services:nationaldataoptout:fhir:rest:read:metadata`|
| `Authorization`      | This will carry the base64 encoded JSON web token required for audit - see [Cross Organisation Audit and Provenance](https://nhsconnect.github.io/FHIR-NOO-API/development_security_jwt.html) for details. |
| `If-None-Exists` | This will check for an existing instance before making creating a new one |


#### Error Handling ####

The Spine will always return a valid capability statement.

### Request Response ###

#### Response Headers ####

No additional headers expected beyond those described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

- The Spine will return a `200` **OK** HTTP status code on successful retrieval of the capabilityStatement profile.

An example capabilityStatement profile is available [here](https://nhsconnect.github.io/FHIR-NOO-API/Examples/NDOP-CapabilityStatement-Example-1.xml) - client systems should always use the CapabilityStatement profile from the above URL as the authoritative capability statement - this is provided as an example for reference only.

