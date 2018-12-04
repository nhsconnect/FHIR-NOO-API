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
|[NDOP-Consent-1](https://fhir.nhs.uk/STU3/StructureDefinition/NDOP-Consent-1) | 
|[Spine-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1) | 

# National Data Opt-out Extensions

|Extension|
|---------|
| [Extension-NDOP-ProxyRole-1](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-ProxyRole-1)|
| [Extension-NDOP-OptOutSource-1](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-OptOutSource-1)|
| [Extension-NDOP-NICReference-1](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-NICReference-1)|

# National Data Opt-out Valuesets

|Valueset|Description|
|-------|-----------|
|[NDOP-OptOutSource-1](https://fhir.nhs.uk/STU3/ValueSet/NDOP-OptOutSource-1)|How the Opt-out preference was set e.g Online, GP, etc.|
|[NDOP-ProxyRole-1](https://fhir.nhs.uk/STU3/ValueSet/NDOP-ProxyRole-1)|The role of a proxy where used to set Opt-out preferences|
|[NDOP-OptOutCategory-1](https://fhir.nhs.uk/STU3/ValueSet/NDOP-OptOutCategory-1)|OPTIONAL Opt-out category to support future Opt-out programmes.|
|[Spine-ErrorOrWarningCode-1](https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1)|Spine error codes|

# National Data Opt-out CodeSystems

|CodeSystem|Description|
|-------|-----------|
|[NDOP-OptOutSource-1](https://fhir.nhs.uk/STU3/CodeSystem/NDOP-OptOutSource-1)|List of Opt-out sources|
|[NDOP-ProxyRole-1](https://fhir.nhs.uk/STU3/CodeSystem/NDOP-ProxyRole-1)|List of approved proxy roles|
|[NDOP-OptOutCategory-1](https://fhir.nhs.uk/STU3/CodeSystem/NDOP-OptOutCategory-1)|List of approved categories|
|[Spine-ErrorOrWarningCode-1](https://fhir.nhs.uk/STU3/CodeSystem/Spine-ErrorOrWarningCode-1)|Spine error codes and descriptions.|

# Identifiers #

| identifier | URI | Comment |
|--------------------------------------------|----------|----|
| `Patient` | https://demographics.spineservices.nhs.uk/STU3/Patient/[NHS Number] | Patient |
|`organization`|https://directory.spineservices.nhs.uk/STU3/Organization/[Org Code] |NHS Digital (X26)|


{% include warning.html content="The URI's on subdomain spineservices.nhs.uk are currently not resolvable, however this will change in the future where references relate to FHIR endpoints in our national systems." %}