---
title: API History
keywords: history, versioning
tags: [history, version]
sidebar: overview_sidebar
permalink: design_product_history.html
summary: History of changes to the National Data Opt-out API.
---
### Version 1.3.1-beta.1

Change to references used by patient and organization. These now include the FHIR version and a FHIR resource e.g https://demographics.spineservices.nhs.uk/STU3/Patient/6101231234

REST examples updated.
Consent example updated.


### Version 1.3.0-beta.1

NDOP now published onto https://fhir.nhs.uk. Links in API now resolvable, with the exception of the spineservice.nhs.uk domain.

URL's changed as follows:

- https://fhir.nhs.uk/STU3/ndop-categories-1 to https://fhir.nhs.uk/STU3/CodeSystem/NDOP-Categories-1
- https://fhir.nhs.uk/STU3/ndop-preference-codes-1 to https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1
- https://fhir.nhs.uk/STU3/opt-out-source-codesystem-1 to https://fhir.nhs.uk/STU3/CodeSystem/NDOP-OptOutSource-1

- https://fhir.nhs.uk/STU3/ValueSet/ndop-category-1 to https://fhir.nhs.uk/STU3/ValueSet/NDOP-Category-1
- https://fhir.nhs.uk/STU3/ValueSet/ndop-preferences-1 to https://fhir.nhs.uk/STU3/ValueSet/NDOP-Preferences-1
- https://fhir.nhs.uk/STU3/ValueSet/opt-out-source-1 to https://fhir.nhs.uk/STU3/ValueSet/NDOP-OptOutSource-1

Consent.Actor example page updated to correct role URL. Now http://hl7.org/fhir/stu3/valueset-security-role-type


### Version 1.2.1-beta.1

Correction to Organization URI.

Added dateTime page, proving example of format and usage.

Improve Me button fixed. 
 
### Version 1.2.0-beta.1 ###

Corrections made to API REST statements.


### Version 1.1.0-beta.1 ###

Subdomain for PDS and SDS agreed. The sub domain of spineservices.nhs.uk will be used to reference FHIR endpoints and details can be found below on its usage within NDOP. Implementation guide updated to reflect this.

- directory.spineservices.nhs.uk
- demographics.spineservices.nhs.uk
- clinicals.spineservices.nhs.uk



### Version 1.0.0-beta.1 ###

Draft beta released to DDC.

### Version 1.0.0-alpha.1 ###

Initial version of the National Data Opt-out API.

