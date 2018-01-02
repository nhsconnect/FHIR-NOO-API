---
title: Cross Organisation Audit & Provenance using JWT
keywords: spine, ssp, integration, audit, jwt, provenance
tags: [Security]
sidebar: overview_sidebar
permalink: development_security_jwt.html
summary: "Overview of how audit and provenance data is expected to be transported over the National Data Opt-out FHIR interfaces using JWT."
---

## Cross Organisation Audit & Provenance using JWT ##

Consumer systems SHALL provide audit and provenance details in the HTTP authorization header as an oAuth bearer token (as outlined in [RFC 6749](https://tools.ietf.org/html/rfc6749){:target="_blank"}) in the form of a JSON Web Token (JWT) as defined in [RFC 7519](https://tools.ietf.org/html/rfc7519){:target="_blank"}.

An example such an HTTP header is given below:

```
     Authorization: Bearer jwt_token_string
```

In future, national authentication and authorisation services will be made available which will issue a bearer token which can be used directly for accessing this API. In the interim however, the client will need to construct the JWT themselves.

It is highly recommended that standard libraries are used for creating the JWT as constructing and encoding the token manually may lead to issues with parsing the token in Spine. A good source of information about JWT and libraries to use can be found on the [JWT.io site](https://jwt.io/)

### JSON Web Token (JWT) ###

Consumer system SHALL generate a new JWT for each API request.

| Claim | Priority | Description | Fixed Value | Dynamic Value | Specification / Example |
|-------|----------|-------------|-------------|---------------|-------------------------|
| iss | R | Client systems issuer URI | No | Yes | |
| sub | R | requesting_patient.identifier.value or requesting_practitioner.identifier.value or requesting_organization.identifier.value | No | Yes | |
| aud | R | Authorization server's `token_URL` | `https://authorize.fhir.nhs.uk/token` | No | |
| exp | R | Expiration time integer after which this authorization MUST be considered invalid. | `exp` | (now + 5 minutes) UTC time in seconds | |
| iat | R | The UTC time the JWT was issued by the requesting system | iat | now UTC time in seconds | |
| reason_for_request | R | Purpose for which access is being requested | `optoutprefs` | No | |
| requested_record | R | The FHIR consent resource being requested | No | FHIR Consent | NDOP-Consent-1 [Rendered](https://fhir.nhs.uk/STU3/StructureDefinition/NDOP-Consent-1)[Example](https://nhsconnect.github.io/FHIR-NOO-API/Examples/Consent-Example-1.xml) |
| requested_scopes | R | Data being requested | `consent/*.[create|read|update]`| No | |
| requesting_device| R | FHIR device resource making the request | No | FHIR Device| Audit-Device-1 [(Rendered)](https://fhir.nhs.uk/StructureDefinition/audit-device-1) [(json)](http://fhir.nhs.uk/StructureDefinition/audit-device-1/_history/1.1?_format=json) [(Example)](Audit/Examples/Device.json) |
| requesting_patient| R | FHIR patient making the request | No | FHIR Patient | Audit-Patient-1 [(Rendered)](https://fhir.nhs.uk/StructureDefinition/audit-patient-1) [(json)](http://fhir.nhs.uk/StructureDefinition/audit-patient-1/_history/1.1?_format=json) [(Example)](Audit/Examples/Patient.json)|
| requesting_organization| R | FHIR organization making the request | No | FHIR Organization | Audit-Organization-1 [(Rendered)](https://fhir.nhs.uk/StructureDefinition/audit-organization-1) [(json)](http://fhir.nhs.uk/StructureDefinition/audit-organization-1/_history/1.1?_format=json) [(Example)](Audit/Examples/Organization.json)|
| requesting_practitioner| R | FHIR practitioner making the request | No | FHIR Practitioner | Audit-Practitioner-1 [(Rendered)](https://fhir.nhs.uk/StructureDefinition/audit-practitioner-1) [(json)](http://fhir.nhs.uk/StructureDefinition/audit-practitioner-1/_history/1.1?_format=json) [(Example - smartcard)](Audit/Examples/Practitioner1a.json) <br /> [(Example - non-smartcard)](Audit/Examples/Practitioner1b.json)|

{% include important.html content="In topologies where consumer applications are provisioned via a portal or middleware hosted by another organisation (e.g. a 'mini service' provider) it is important for audit purposes that the practitioner and organisation populated in the JWT reflect the originating organisation rather than the hosting organisation. Where a patient is the consumer of the application, they will be populated in the JWT." %}


#### JWT Generation ####
Consumer systems SHALL generate the JSON Web Token (JWT) consisting of three parts separated by dots (.), which are:

- Header
- Payload
- Signature

Consumer systems SHALL generate an Unsecured JSON Web Token (JWT) using the "none" algorithm parameter in the header to indicate that no digital signature or MAC has been performed (please refer to section 3.6 of RFC 7513 for details).

```json
{
  "alg": "none",
  "typ": "JWT"
}
```

Consumer systems SHALL generate an empty signature.

The final output is three Base64 strings separated by dots (note - there is some canonicalisation done to the JSON before it is base64 encoded, which the JWT code libraries will do for you).

For example:

```shell
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJodHRwczovL1tDb25zdW1lclN5c3RlbVVSTF0iLCJzdWIiOiJbQWN0b3JSZWZlcmVuY2VdIiwiYXVkIjoiaHR0cHM6Ly9hdXRob3JpemUuZmhpci5uaHMudWsvdG9rZW4iLCJleHAiOjE0Njk0MzY5ODcsImlhdCI6MTQ2OTQzNjY4NywicmVhc29uX2Zvcl9yZXF1ZXN0Ijoib3B0b3V0cHJlZnMiLCJyZXF1ZXN0ZWRfcmVjb3JkIjp7InJlc291cmNlVHlwZSI6IkNvbnNlbnQiLCJwYXRpZW50IjpbeyJyZWZlcmVuY2UiOiJodHRwczovL2RlbW9ncmFwaGljcy5zcGluZXNlcnZpY2VzLm5ocy51ay9TVFUzL1BhdGllbnQvW25ocy1udW1iZXJdIn1dfSwicmVxdWVzdGVkX3Njb3BlcyI6ImNvbnNlbnQvKi5yZWFkIiwicmVxdWVzdGluZ19kZXZpY2UiOnsicmVzb3VyY2VUeXBlIjoiRGV2aWNlIiwiaWQiOiJbRGV2aWNlSURdIiwiaWRlbnRpZmllciI6W3sic3lzdGVtIjoiW0RldmljZVN5c3RlbV0iLCJ2YWx1ZSI6IltEZXZpY2VJRF0ifV0sInR5cGUiOiJbU05PTUVEQ1RDb2RlRm9yVHlwZU9mRGV2aWNlXSIsIm1vZGVsIjoiW1NvZnR3YXJlTmFtZV0iLCJ2ZXJzaW9uIjoiW1NvZnR3YXJlVmVyc2lvbl0ifSwicmVxdWVzdG9yX2lkZW50aXR5IjoiW1JlcXVlc3RvcklEXSIsInJlcXVlc3RpbmdfYWN0b3IiOiJbQWN0b3JSZWZlcmVuY2VdIn0.
```

{% include tip.html content="The [JWT.io](https://jwt.io/) website includes a number of rich resources to aid in developing JWT enabled applications." %}

## JWT Payload Example ##

```json
{
	"iss": "https://www.nhs.uk",
	"sub": "National Data Opt-out Preferences",
	"aud": "https://authorize.fhir.nhs.uk/token",
	"exp": 1469436987,
	"iat": 1469436687,
	"reason_for_request": "optoutprefs",
	"requested_record": {
		"resourceType": "Consent",
		"patient": [{
			"reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/6101231234"
		}]
	},
	"requested_scopes": "consent/*.read",
	"requesting_device": {
		"resourceType": "Device",
		"id": "009f0bf0-d434-11e6-9598-0800200c9a66",
		"meta": {
			"profile": [
				"https://fhir.nhs.uk/StructureDefinition/audit-device-1"
			]
		},
		"identifier": [{
			"id": "0b7677c0-d434-11e6-9598-0800200c9a66"
		}],
		"type": {
			"coding": [{
				"system": "http://snomed.info/sct",
				"code": "462240000",
				"display": "Patient health record information system (physical object)"
			}]
		},
		"model": "AA 1001-C",
		"version": "8.15-04"
	},
	"requesting_organization": {
		"resourceType": "Organization",
		"id": "1a9f3c50-d434-11e6-9598-0800200c9a66",
		"meta": {
			"profile": [
				"https://fhir.nhs.uk/StructureDefinition/audit-organization-1"
			]
		},
		"identifier": [{
			"system": "https://fhir.nhs.uk/Id/ods-organization-code",
			"value": "R1A02"
		}],
		"name": "King's College Hospital"
	},
	"requesting_practitioner": {
		"resourceType": "Practitioner",
		"id": "3516e6a0-d434-11e6-9598-0800200c9a66",
		"identifier": [{
			"system": "https://fhir.nhs.uk/Id/local-practitioner-identifier",
			"value": "123456"
		}]
	}
}
```

{% include important.html content="Whilst the use of a JWT and the claims naming is inspired by the [SMART on FHIR](https://github.com/smart-on-fhir/smart-on-fhir.github.io/wiki/cross-organizational-auth) NHS Digital hasn't committed to using the SMART on FHIR specification." %}





