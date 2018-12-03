---
title: Consent REST
keywords: Consent, REST, interactions
tags: [consent,REST,usage]
sidebar: overview_sidebar
permalink: build_consent_restful.html
summary: "REST interactions that can be used within NDOP API"
---
## National Data Opt-out Spine RESTful Interaction Diagram ##

The diagram below demonstrates the REST interactions between a client and the NDOP FHIR server. This is intended to provide a high level view of how the client/server interaction operates within the NDOP environment.

<img src="images/NDOPInteractions2.png">

{% include important.html content="To prevent duplicate NDOP resources for a patient, implementers MUST perform a search prior to a create, to check for an existing instance."%}

<a name="section1"></a>

## 1. Check for any existing National Data Opt-out resource ##

Prior to creating a Consent resource, a check MUST be carried out against that patient to determine if any Consent resources currently exist, to prevent duplication of resources.

- ***Sender:*** Any NDOP client
- ***Receiver:*** Spine 2

```
GET https://[baseUrl]/Consent?patient=https://demographics.spineservices.nhs.uk/STU3/Patient/6105551233
``` 

**Responses**

Where a resource does not exist:

- HTTP 200-Request was successfully executed
- Bundle resource of type *searchset* containing a total value of 0 Consent resources.

This would indicate it is safe to create a Consent resource for this patient. See [section 2](#section2) for register interaction. 

Example below demonstrates a response where no resource exists using XML. JSON example can be viewed here [(Bundle)](Examples/NDOP-Bundle-Searchset-Example-1.json)

```xml
<Bundle xmlns="http://hl7.org/fhir">
	<id value="de258b7f-2f0b-4b41-afcb-964d9995fd4f"/>
	<meta>
		<versionId value="8c8263ee-f582-4d08-bf84-46d016127552"/>
		<lastUpdated value="2017-11-16T11:18:41.61+00:00"/>
	</meta>
	<type value="searchset"/>
	<total value="0"/>
	<link>
		<relation value="self"/>
		<url value="http://localhost:4080/Consent?patient=https://demographics.spineservices.nhs.uk/STU3/Patient/6105551233&amp;_format=xml"/>
	</link>
</Bundle>
```

Where a resource does exist:

- HTTP 200-Request was successfully executed
- Bundle resource of type *searchset* containing a maximum total value 1 Consent resource.
- The existence of a resource requires an update interaction to overwrite the existing old resource with a new version. The previous version will become historic. See the section titled [Update Patient’s Existing National Data Opt-out Preferences Interaction](#section3) for information on updating an existing consent resource using logical id.

Example of bundle section containing searchset in XML. Note that <id> in this section is the bundle id and NOT the consent id:

<script src="https://gist.github.com/IOPS-DEV/543abe076ce20ff348a7d244f42308b2.js"></script>

<a id="section1"></a>

The remaining section of the same XML contains the Consent resource for the patient. 

The `<id>` here is the unique logical id for the consent resource:

<script src="https://gist.github.com/IOPS-DEV/a65f8f6e775f7c7c6cd3aa1bd340ef1d.js"></script>

Full JSON example can be viewed [(here)](Examples/NDOP-Bundle-Searchset-Example-2.json). 

<a name="section2"></a>

## 2. Register Patient's National Data Opt-out Preferences Interaction ##

Where an existing Consent resource does not exist, the client system will construct an XML body containing NDOP preferences and submit this to the Spine using a RESTful create interaction.

- ***Sender:*** Any NDOP client
- ***Receiver:*** Spine 2

```
POST https://[baseUrl]/Consent
```

{% include note.html content="Details on the FHIR RESTful specification for creating a new instance can be found here [RESTful Create](https://www.hl7.org/fhir/http.html#create)" %}

An XML example of a new resource is displayed below. JSON example can be viewed [(here)](Examples/Consent-Example-1.json)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Consent xmlns="http://hl7.org/fhir">
	<meta>
		<profile value="https://fhir.nhs.uk/STU3/StructureDefinition/NDOP-Consent-1"/>
	</meta>
	<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-OptOutSource-1">
		<valueCodeableConcept>
			<coding>
				<system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-OptOutSource-1"/>
				<code value="OP"/>
				<display value="Online Portal"/>
			</coding>
		</valueCodeableConcept>
	</extension>
	<status value="active"/>
	<patient>
		<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
	</patient>
	<dateTime value="2017-12-14T11:15:33+00:00"/>
		<consentingParty>
		<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
	</consentingParty>
	<organization>
		<reference value="https://directory.spineservices.nhs.uk/STU3/Organization/X26"/>
	</organization>
	<policy>
		<authority value="https://www.gov.uk/"/>
		<uri value="https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.PDF"/>
	</policy>
	<purpose>
		<system value="https://snomed.info/sct"/>
		<code value="370856009"/>
		<display value="Limiting access to confidential patient information"/>
	</purpose>
</Consent>
```

---
**Responses**

Success:

Assuming successful HTTP POST, there are several possible responses to the NDOP request:

- HTTP 201-Record Created: The entry has been successfully created and the NDOP returns an HTTP Location header containing the 'server' assigned logical Id of the created resource.

Failure:

- SHALL return one of the below HTTP status error codes with an OperationOutcome resource that conforms to the `Spine-OperationOutcome-1` profile if the update cannot be executed.
- The below table summarises the types of error that could occur, and the HTTP response codes, along with the values to expect in the OperationOutcome response body.
 
|HTTP Code|issue-severity|issue-type|Details.Code|Details.Display|
|---------|--------------|----------|------------|---------------|
|405|error|forbidden|MSG_RESOURCE_ID_FAIL|Client is not permitted to assign an id|
|422|error|duplicate|DUPLICATE_REJECTED|Consent already exists for this patient/policy/purpose|

**Response Spine-OperationOutcome-1 XML Example**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<OperationOutcome">
<id value="f19e4165-b379-4377-ad43-df65f609eba5"/>
<meta>
	<profile value="https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"/>
</meta>
<issue>
	<severity value="error"/>
	<code value="forbidden"/>
	<details>
		<coding>
			<system value="https://fhir.nhs.uk/STU3/CodeSystem/Spine-ErrorOrWarningCode-1"/>
			<code value="MSG_RESOURCE_ID_FAIL"/>
			<display value="Client is not permitted to assign an id"/>
		</coding>
	</details>
	<diagnostics value="An attempted has been made to create a new consent record that includes an id."
</issue>
</OperationOutcome>
```

JSOn example can be viewed JSON example can be viewed [(here)](Examples/Spine-OperationOutcome-1-Example-1.json)
<a name="section3"></a>

{% include warning.html content="Once a logical id has been assigned to the consent resource, it is immutable. Any updates to the consent preferences will use this logical id" %}

## 3. Update Patient's Existing National Data Opt-out Preferences Interaction ##

Where a Consent resource exists, the client system will perform a REST update interaction to amend the patient's National Data Opt-out preferences and submit a revised body to the NDOP service. The [logical id](#section1) from the searchset result described in the section titled ['Check for any existing National Data Opt-out resource'](#section1) is used in the REST statement, to identify the patient resource to be updated and MUST be included in the updated XML body.

- ***Sender:***Any NDOP Client
- ***Receiver:***Spine 2

```
PUT https://[base url]/Consent/[logical id] 
```

The entire XML body will be replaced with a new version to include one or more changes, in addition to the <id> element. Unchanged data MUST still be included.

Example of updated Consent resource body from example provided in section titled [Check for any existing National Data Opt-out resource](#section1). Only status has changed from active to inactive, and dateTime updated with date and time of update. All other data remains unchanged.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Consent xmlns="http://hl7.org/fhir">
	<meta>
		<profile value="https://fhir.nhs.uk/STU3/StructureDefinition/NDOP-Consent-1"/>
	</meta>
	<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-OptOutSource-1">
		<valueCodeableConcept>
			<coding>
				<system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-OptOutSource-1"/>
				<code value="OP"/>
				<display value="Online Portal"/>
			</coding>
		</valueCodeableConcept>
	</extension>
	<status value="inactive"/>
	<patient>
		<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
	</patient>
	<dateTime value="2017-12-19T11:15:33+00:00"/>
		<consentingParty>
		<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
	</consentingParty>
	<organization>
		<reference value="https://directory.spineservices.nhs.uk/STU3/Organization/X26"/>
	</organization>
	<policy>
		<authority value="https://www.gov.uk/"/>
		<uri value="https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.PDF"/>
	</policy>
	<purpose>
		<system value="https://snomed.info/sct"/>
		<code value="370856009"/>
		<display value="Limiting access to confidential patient information"/>
	</purpose>
</Consent>
```

{% include note.html content="Details on the FHIR RESTful specification for creating a new instance can be found here [RESTful Update](https://www.hl7.org/fhir/http.html#update)" %}

**Responses**

Assuming successful HTTP PUT, there are several possible responses to the NDOP request:

- HTTP 200-OK: The entry has been successfully updated and the NDOP returns an HTTP Location header containing the 'server' assigned logical Id of the updated resource.
- HTTP 400-Bad Request: Resource could not be parsed or failed basic FHIR validation rules
- HTTP 404-Resource Not Found: An atempted was made to update a resource which does not exist. 
- HTTP 422-Unprocessable Entity: The proposed resource violated applicable FHIR profiles or server business rules.


## 4. Retrieve Patient's National Data Opt-out Preferences Interaction ##

The client system performs a RESTful search interaction for current patient preferences located on the National Data Opt-out service.

- ***Sender:***Any NDOP Client
- ***Receiver:***Spine 2
 
```
GET https://[base url]/Consent[parameters] 
```

{% include note.html content="Details on the FHIR RESTful specification for reading an instance can be found here [RESTful Read](https://www.hl7.org/fhir/http.html#read)" %}
---
**Responses**

The search results **MAY** return 1 or zero resource for the patient's National Data Opt-out preferences.

Assuming successful HTTP POST, there is one possible outcome to a search request:

- HTTP 200-Request was successfully executed

The NDOP FHIR server determines which of the set of resources it serves meet the specific criteria, and returns the results of the search in the HTTP response as a 'searchset' bundle or as single consent resource.

Note: Although an HTTP response 200 OK indicates the request was successful, the bundle could return a 0 (zero) total value indicating no resources were found. An XML example of a Bundle with a 0 (zero) total value indicating no resource was found is shown below.

```xml
<Bundle xmlns="http://hl7.org/fhir">
	<id value="12a2d9da-8b92-40b4-a978-c71d7f20bdb3"/>
	<meta>
		<versionId value="3d754ff8-2ff8-4807-97ed-07449e14d263"/>
		<lastUpdated value="2017-11-14T13:55:37.661+00:00"/>
	</meta>
	<type value="searchset"/>
	<total value="0"/>
	<link>
		<relation value="self"/>
		<url value="http://demographics.spineservices.nhs.uk/Consent?patient=https://demographics.spineservices.nhs.uk//45055771aaaa&amp;_format=xml"/>
	</link>
</Bundle>
```

## 5. Additional REST Examples ##

**XML Example 1**

The example below demonstrates the structure of a constructed XML body that can be submitted to the National Data Opt-out service via a HTTP POST. 

<script src="https://gist.github.com/IOPS-DEV/49fa92287f5b1f05cf451a2f2466a77f.js"></script>

{% include custom/post.consent.html base="[baseUrl]/" resource="Consent" content1="POST" text1="https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104"%}

{% include warning.html content="To prevent duplicate NDOP instances for a patient, implementers MUST perform a search prior to a create, to check for an existing instance, or use a conditional create for creating new instances."%}


{% include custom/get.consent.html base="[baseUrl]/" resource="Consent" content2="GET" id="133552f9-7aaf-485f-a91a-bdfc0a367409" nhsno="https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104" text3="370856009"%}

{% include custom/put.consent.html base="[baseUrl]/" resource="Consent" content2="PUT" id="133552f9-7aaf-485f-a91a-bdfc0a367409"%}

## Searching National Data Opt-out History ##

{% include custom/history.consent.html base="[baseUrl]/" resource="Consent" content2="GET" id="785f7cc6-f63b-41fc-9bd4-2d09df5606f9" text1="https://demographics.spineservices.nhs.uk/STU3/Patient/4505577104" text2="370856009" histid="6ed33184-56ab-450f-98c5-8f86d7310766"%}