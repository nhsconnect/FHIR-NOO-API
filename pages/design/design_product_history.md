---
title: API History
keywords: history, versioning
tags: [history, version]
sidebar: overview_sidebar
permalink: design_product_history.html
summary: History of changes to the National Data Opt-out API.
---
### Version 1.5.0-alpha.0

- Category is no longer a requirement for NDOP API and has been removed from guide
- Correction to REST history syntax 
- Added generic assure, test and deploy pages used across all APIs

### Version 1.4.0-alpha.0

- Release date removed from IG
- Grammatical corrections made throughout guide
- Consent elements updated with clearer descriptions
- Correction to Online Portal code used in an example.
- Correction to example showing incorrect purpose code.
- REST history description updated
- The use of `If-None_exists` header removed from API. conditionalCreate is therefore not supported.
- capabilityStatement description has been revised to provide improved clarity
- Interaction section has been revised, adding detail and XML snippets to make it clear to implementers how the API interacts between the client and server 
- Missing Consent XML example added
- Reference section had logical id as a URL. Now removed.
- Correction to Practitioner identifier URL

### Version 1.3.1-alpha.0

Change to references used by patient and organization. These now include the FHIR version and a FHIR resource e.g https://demographics.spineservices.nhs.uk/STU3/Patient/6101231234

REST examples updated.
Consent example updated.


### Version 1.3.0-alpha.0

NDOP now published onto https://fhir.nhs.uk. Links in API now resolvable, with the exception of the spineservice.nhs.uk domain.

URL's changed as follows:

- https://fhir.nhs.uk/STU3/ndop-categories-1 to https://fhir.nhs.uk/STU3/CodeSystem/NDOP-Categories-1
- https://fhir.nhs.uk/STU3/ndop-preference-codes-1 to https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1
- https://fhir.nhs.uk/STU3/opt-out-source-codesystem-1 to https://fhir.nhs.uk/STU3/CodeSystem/NDOP-OptOutSource-1

- https://fhir.nhs.uk/STU3/ValueSet/ndop-category-1 to https://fhir.nhs.uk/STU3/ValueSet/NDOP-Category-1
- https://fhir.nhs.uk/STU3/ValueSet/ndop-preferences-1 to https://fhir.nhs.uk/STU3/ValueSet/NDOP-Preferences-1
- https://fhir.nhs.uk/STU3/ValueSet/opt-out-source-1 to https://fhir.nhs.uk/STU3/ValueSet/NDOP-OptOutSource-1

Consent.Actor example page updated to correct role URL. Now http://hl7.org/fhir/stu3/valueset-security-role-type


### Version 1.2.1-alpha.0

Correction to Organization URI.

Added dateTime page, proving example of format and usage.

Improve Me button fixed. 
 
### Version 1.2.0-alpha.0 ###

Corrections made to API REST statements.


### Version 1.1.0-alpha.0 ###

Subdomain for PDS and SDS agreed. The sub domain of spineservices.nhs.uk will be used to reference FHIR endpoints and details can be found below on its usage within NDOP. Implementation guide updated to reflect this.

- directory.spineservices.nhs.uk
- demographics.spineservices.nhs.uk
- clinicals.spineservices.nhs.uk



### Version 1.0.0-alpha.0 ###

Draft beta released to DDC.

### Version 1.0.0-alpha.0 ###

Initial version of the National Data Opt-out API.

