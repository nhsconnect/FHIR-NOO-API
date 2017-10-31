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
| requested_record | R | The FHIR consent resource being requested (i.e. NHS Number identifier details) | No | FHIR Consent | Consent-1[Rendered](https://fhir.nhs.uk/STU3/StructureDefinition/NDOP-Consent-1)[Example](https://github.com/nhsconnect/FHIR-NOO-API/Examples/Consent-Example-1.xml) |
| requested_scopes | R | Data being requested | consent.read | No | |
| requesting_actor | R | Reference to the person who is making the request | No | Reference | https://directory.spineservices.nhs.uk/E12345 | |


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
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJpc3MiOiJodHRwOi8vZWMyLTU0LTE5NC0xMDktMTg0LmV1LXdlc3QtMS5jb21wdXRlLmFtYXpvbmF3cy5jb20vIy9zZWFyY2giLCJzdWIiOiIxIiwiYXVkIjoiaHR0cHM6Ly9hdXRob3JpemUuZmhpci5uaHMubmV0L3Rva2VuIiwiZXhwIjoxNDgxMjUyMjc1LCJpYXQiOjE0ODA5NTIyNzUsInJlYXNvbl9mb3JfcmVxdWVzdCI6ImRpcmVjdGNhcmUiLCJyZXF1ZXN0ZWRfcmVjb3JkIjp7InJlc291cmNlVHlwZSI6IlBhdGllbnQiLCJpZGVudGlmaWVyIjpbeyJzeXN0ZW0iOiJodHRwOi8vZmhpci5uaHMubmV0L0lkL25ocy1udW1iZXIiLCJ2YWx1ZSI6IjkwMDAwMDAwMzMifV19LCJyZXF1ZXN0ZWRfc2NvcGUiOiJwYXRpZW50LyoucmVhZCIsInJlcXVlc3RpbmdfZGV2aWNlIjp7InJlc291cmNlVHlwZSI6IkRldmljZSIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6IldlYiBJbnRlcmZhY2UiLCJ2YWx1ZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn1dLCJtb2RlbCI6IkRlbW9uc3RyYXRvciIsInZlcnNpb24iOiIxLjAifSwicmVxdWVzdGluZ19vcmdhbml6YXRpb24iOnsicmVzb3VyY2VUeXBlIjoiT3JnYW5pemF0aW9uIiwiaWQiOiIxIiwiaWRlbnRpZmllciI6W3sic3lzdGVtIjoiaHR0cDovL2ZoaXIubmhzLm5ldC9JZC9vZHMtb3JnYW5pemF0aW9uLWNvZGUiLCJ2YWx1ZSI6IltPRFNDb2RlXSJ9XSwibmFtZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn0sInJlcXVlc3RpbmdfcHJhY3RpdGlvbmVyIjp7InJlc291cmNlVHlwZSI6IlByYWN0aXRpb25lciIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6Imh0dHA6Ly9maGlyLm5ocy5uZXQvc2RzLXVzZXItaWQiLCJ2YWx1ZSI6IkcxMzU3OTEzNSJ9LHsic3lzdGVtIjoibG9jYWxTeXN0ZW0iLCJ2YWx1ZSI6IjEifV0sIm5hbWUiOnsiZmFtaWx5IjpbIkRlbW9uc3RyYXRvciJdLCJnaXZlbiI6WyJHUENvbm5lY3QiXSwicHJlZml4IjpbIk1yIl19fX0.
```

{% include tip.html content="The [JWT.io](https://jwt.io/) website includes a number of rich resources to aid in developing JWT enabled applications." %}

## JWT Payload Example ##

```json
{
	"iss": "https://[ConsumerSystemURL]",
	"sub": "[ActorID]",
	"aud": "https://authorize.fhir.nhs.uk/token",
	"exp": 1469436987,
	"iat": 1469436687,
	"reason_for_request": "optoutprefs",
	"requested_record": {
		"resourceType": "Consent",
		"patient": [{
			"reference": "https://demographics.spineservices.nhs.uk/[nhs-number]"
		}]
	},
	"requested_scopes": "consent/*.read",
	"requesting_actor": "https://[reference]"
}
```

{% include important.html content="Whilst the use of a JWT and the claims naming is inspired by the [SMART on FHIR](https://github.com/smart-on-fhir/smart-on-fhir.github.io/wiki/cross-organizational-auth) NHS Digital hasn't commited to using the SMART on FHIR specification." %}





