---
title: Cross Organisation Audit & Provenance using JWT
keywords: spine, ssp, integration, audit, jwt, provenance
tags: [Security]
sidebar: overview_sidebar
permalink: development_security_jwt.html
summary: "Overview of how audit and provenance data is expected to be transported over the National Data Opt-out FHIR interfaces using JWT."
---

## Cross Organisation Audit & Provenance using JWT ##

Consumer systems SHALL provided audit and provenance details in the HTTP authorization header as an oAuth bearer token (as outlined in [RFC 6749](https://tools.ietf.org/html/rfc6749){:target="_blank"}) in the form of a JSON Web Token (JWT) as defined in [RFC 7519](https://tools.ietf.org/html/rfc7519){:target="_blank"}.

### JSON Web Token (JWT) ###

Consumer system SHALL generate a new JWT for each API request.

| Claim | Priority | Description | Fixed Value | Dynamic Value | Specification / Example |
|-------|----------|-------------|-------------|---------------|-------------------------|
| iss | R | Client systems issuer URI | No | Yes | |
| sub | R | ID for the actor who is issuing this request. Matches `requesting_actor.actor.reference` or `requesting_actor.actor.reference.ActorPerson` | No | Yes | |
| aud | R | Authorization server's `token_URL` | `https://authorize.fhir.nhs.uk/token` | No | |
| exp | R | Expiration time integer after which this authorization MUST be considered invalid. | `exp` | (now + 5 minutes) UTC time in seconds | |
| iat | R | The UTC time the JWT was issued by the requesting system | iat | now UTC time in seconds | |
| reason_for_request | R | Purpose for which access is being requested | `optoutprefs` | No | |
| requested_record | R | The FHIR consent resource being requested (i.e. NHS Number identifier details) | No | FHIR Consent | Consent-1 [Rendered](https://fhir.nhs.uk/STU3/StructureDefinition/NDOP-Consent-1)[Example](https://nhsconnect.github.io/FHIR-NOO-API/Examples/Consent-Example-1.xml) |
| requested_scopes | R | Data being requested | consent.read | No | |
| requesting_device| R | FHIR device resource making the request | No | FHIR Device| TODO |
| requestor_identity | R | Identity of the person or organization making request | No | NHS Number or ODS Code | TODO | 
| requesting_actor | R | Reference to the person who is making the request | No | Reference | | |


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
	"iss": "https://[ConsumerSystemURL]",
	"sub": "[ActorReference]",
	"aud": "https://authorize.fhir.nhs.uk/token",
	"exp": 1469436987,
	"iat": 1469436687,
	"reason_for_request": "optoutprefs",
	"requested_record": {
		"resourceType": "Consent",
		"patient": [{
			"reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/[nhs-number]"
		}]
	},
	"requested_scopes": "consent/*.read",
	"requesting_device": {
		"resourceType": "Device",
		"id": "[DeviceID]",
		"identifier": [{
			"system": "[DeviceSystem]",
			"value": "[DeviceID]"
		}],
		"type": "[SNOMEDCTCodeForTypeOfDevice]",
		"model": "[SoftwareName]",
		"version": "[SoftwareVersion]"
	},
	"requestor_identity": "[RequestorID]",
	"requesting_actor": "[ActorReference]"
}
```

{% include important.html content="Whilst the use of a JWT and the claims naming is inspired by the [SMART on FHIR](https://github.com/smart-on-fhir/smart-on-fhir.github.io/wiki/cross-organizational-auth) NHS Digital hasn't committed to using the SMART on FHIR specification." %}





