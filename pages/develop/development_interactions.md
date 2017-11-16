---
title: Interactions
keywords: interaction, consent
tags: [interaction]
sidebar: overview_sidebar
permalink: development_interactions.html
summary: "National Data Opt-out Spine Interactions"
---

## National Data Opt-out Spine RESTful Interaction Diagram ##

<img src="images/NDOPInteractions2.png">

{% include important.html content="To prevent duplicate NDOP instances for a patient, implementers MUST perform a search prior to a create, to check for an existing instance, or use a [conditional create](https://www.hl7.org/fhir/http.html#ccreate) for creating new instances."%}

## 1. Check for any existing National Data Opt-out record ##

Prior to creating an NDOP record, a check MUST be carried out to determine if any Consent records currently exist to prevent duplication of records.

- ***Sender:*** Any NDOP client
- ***Receiver:*** Spine 2
- ***RESTful API Interaction:*** GET https://fhir.nhs.uk/STU3/Consent?patient=https://demographics.spineservices.nhs.uk/STU3/Patient/6105551233
 
Note: This interaction will search for any live Consent records. To limit this, a purpose code MAY be used e.g. GET https://fhir.nhs.uk/STU3/Consent?patient=https://demographics.spineservices.nhs.uk/STU3/Patient/6105551233&purpose=PLAN

**Responses**

Where a record does not exist:

- HTTP 200-Request was successfully executed
- Bundle resource of type *searchset* containing a total value of 0 Consent resources.

This would indicate it is safe to create a Consent record for this patient. See section 2 for register interaction. Example below demonstrates a response where no record exists 

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

<details><summary>CLICK ME</summary>
<p>

#### yes, even hidden code blocks!

```python
print("hello world!")
```

</p>
</details>

Where a record does exist:

- HTTP 200-Request was successfully executed
- Bundle resource of type *searchset* containing a total value of 1 Consent record, which would contain the unique logical id for this record.
- The existence of a record requires an update interaction to overwrite the existing old record with a new version. The previous version will become historic. See section 3 for updating an existing consent record using logical id.

## 2. Register Patients National Data Opt-out Preferences Interaction ##

Where an existing NDOP record does not exist, the client system will construct a XML body containing NDOP preferences and submit this to the ACS via Spine services using a RESTful create interaction.

- ***Sender:*** Any NDOP client
- ***Receiver:*** Spine 2
- ***RESTful API Interaction:*** POST https://fhir.nhs.uk/Consent


{% include note.html content="Details on the FHIR RESTful specification for creating a new instance can be found here [RESTful Create](https://www.hl7.org/fhir/http.html#create)" %}

---
**Responses**

Assuming successful URL submission, there are several possible responses to the NDOP request:

- HTTP 201-Record Created: The entry has been successfully created and the NDOP returns an HTTP Location header containing the 'server' assigned logical Id of the created resource.
- HTTP 400-Bad Request: Resource could not be parsed or failed basic FHIR validation rules
- HTTP 422-Unprocessable Entity: The proposed resource violated applicable FHIR profiles or server business rules.

## 3. Update Patients Existing National Data Opt-out Preferences Interaction ##

Where an existing Consent record exists, the client system will perform a RESTful update interaction to amend the patients National Data Opt-out preferences and submit a revised body to the NDOP service. The logical id from the searchset result in section 1 is used to update the record.

- ***Sender:***Any NDOP Client
- ***Receiver:***Spine 2
- ***RESTful API Interaction:***PUT https://[baseurl]/Consent/[logical id] 

The entire XML body will be replaced with a new version to include one or more changes. Unchanged data MUST still be included.

{% include note.html content="Details on the FHIR RESTful specification for creating a new instance can be found here [RESTful Update](https://www.hl7.org/fhir/http.html#update)" %}

**Responses**

Assuming successful URL submission, there are several possible responses to the NDOP request:

- HTTP 200-OK: The entry has been successfully updated and the NDOP returns an HTTP Location header containing the 'server' assigned logical Id of the updated resource.
- HTTP 400-Bad Request: Resource could not be parsed or failed basic FHIR validation rules
- HTTP 422-Unprocessable Entity: The proposed resource violated applicable FHIR profiles or server business rules.


## 4. Retrieve Patients National Data Opt-out Preferences Interaction ##

The client system will perform a RESTful search interaction for current patient preferences located on the National Data Opt-out service.

- ***Sender:***Any NDOP Client
- ***Receiver:***Spine 2
- ***RESTful API Interaction:***GET https://[baseurl]/Consent[parameters] 


{% include note.html content="Details on the FHIR RESTful specification for reading an instance can be found here [RESTful Read](https://www.hl7.org/fhir/http.html#read)" %}
---
**Responses**

The search results **shall** return one or two instances of the patients National Data Opt-out preferences, depending on search parameters utilized. Each instance **shall** have one of the following preferences:

- RESCH - Research Opt-Out
- PLAN - Planning and Commissioning Opt-Out

Assuming successful URL submission, there is one possible outcome to a search request:

- HTTP 200-Request was successfully executed

The NDOP FHIR server determines which of the set of resources it serves meet the specific criteria, and returns the results of the search in the HTTP response as a 'searchset' bundle or as single consent resource.

Note: Although an HTTP response 200 OK indicates the request was successful, the bundle could return a 0 (zero) total value indicating no record was found. An XML example of a Bundle with a 0 (zero) total value indicating no record was found is shown below.

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
		<url value="http://localhost:4080/Consent?patient=https://demographics.spineservices.nhs.uk//45055771aaaa&amp;_format=xml"/>
	</link>
</Bundle>
```

