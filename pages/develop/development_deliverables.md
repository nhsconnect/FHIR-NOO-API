---
title: National Data Opt-out | Reference
keywords: development Reference
tags: [development]
sidebar: overview_sidebar
permalink: development_deliverables.html
summary: "Developer Cheat Sheet shortcuts for the <br/>technical build of National Data Opt-out API."
---

{% include important.html content="[Simplifier.net](https://simplifier.net/NOOM/~introduction) is used to as a temporary solution to provide rendered profiles until the fhir.nhs.uk server is updated to support STU3 rendered profiles. The links below will only resolve once this work has been completed."%}

# National Data Opt-out Profiles:

|Profile| 
|-------|
| [NDOP-Consent-1](https://simplifier.net/NOOM/Consent) | 

# National Data Opt-out Extensions

|Extension|
|---------|
| [Extension-ActorPerson-1](https://simplifier.net/NOOM/extension-actorperson-1)|
| [Extension-Extension-Opt-out-Source-1](https://simplifier.net/NOOM/extension-optoutsource-1)|


# National Data Opt-out Valesets

|Valeset|Description|
|-------|-----------|
|[ndop-category-1](https://simplifier.net/NOOM/category-1)|
|[ndop-preferences-1](https://simplifier.net/NOOM/preferences-1)|
|[Opt-Out-Source](https://simplifier.net/NOOM/opt-out-source-1)|

# Identifiers #

| identifier | URI | Comment |
|--------------------------------------------|----------|----|
| `Logical ID` | https://fhir.nhs.uk/Consent/[id] | Consent record identifier |
| `Patient` | https://demographics.spineservices.nhs.uk | Patient |
|`actor`|https://clinicals.spineservices.nhs.uk or https://demographics.spineservices.nhs.uk | Patient or Practitioner|
|`organization`|https://clinicals.spineservices.nhs.uk |NHS Digital (X26)|


{% include warning.html content="The URI's on subdomain spineservices.nhs.uk are currently not resolvable, however this will change in the future where references relate to FHIR endpoints in our national systems." %}