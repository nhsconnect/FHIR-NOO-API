---
title: National Data Opt-out | Reference
keywords: development Reference
tags: [development]
sidebar: overview_sidebar
permalink: development_deliverables.html
summary: "Developer Cheat Sheet shortcuts for the technical build of National Data Opt-out API."
---

# National Data Opt-out Profiles:

|Profile| 
|-------|
| [NDOP-Consent-1](https://fhir.nhs.uk/STU3/StructureDefinition/NDOP-Consent-1) | 

# National Data Opt-out Extensions

|Extension|
|---------|
| [Extension-NDOP-ActorPerson-1](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-ActorPerson-1)|
| [Extension-NDOP-OptOutSource-1](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-OptOutSource-1)|


# National Data Opt-out Valuesets

|Valueset|Description|
|-------|-----------|
|[NDOP-Preferences-1](https://fhir.nhs.uk/STU3/ValueSet/NDOP-Preferences-1)|
|[NDOP-OptOutSource-1](https://fhir.nhs.uk/STU3/ValueSet/NDOP-OptOutSource-1)|

# National Data Opt-out CodeSystems

|CodeSystem|Description|
|-------|-----------|
|[NDOP-PreferencesCodes-1](https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1)|
|[NDOP-OptOutSource-1](https://fhir.nhs.uk/STU3/CodeSystem/NDOP-OptOutSource-1)|

# Identifiers #

| identifier | URI | Comment |
|--------------------------------------------|----------|----|
| `Patient` | https://demographics.spineservices.nhs.uk/STU3/Patient/[NHS Number] | Patient |
|`actor`|https://demographics.spineservices.nhs.uk/STU3/Patient/[NHS Number] or https://directory.spineservices.nhs.uk/STU3/Practitioner/[Org Code] | Patient or Practitioner|
|`organization`|https://directory.spineservices.nhs.uk/STU3/Organization/[Org Code] |NHS Digital (X26)|


{% include warning.html content="The URI's on subdomain spineservices.nhs.uk are currently not resolvable, however this will change in the future where references relate to FHIR endpoints in our national systems." %}