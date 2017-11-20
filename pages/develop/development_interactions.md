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

Prior to creating a Consent record, a check MUST be carried out against that patient to determine if any Consent records currently exist, to prevent duplication of records.

- ***Sender:*** Any NDOP client
- ***Receiver:*** Spine 2
- ***RESTful API Interaction:*** GET https://fhir.nhs.uk/STU3/Consent?patient=https://demographics.spineservices.nhs.uk/STU3/Patient/6105551233
 
**Note:** This interaction will search for any live Consent records. To limit this, a purpose code MAY be used e.g. GET https://fhir.nhs.uk/STU3/Consent?patient=https://demographics.spineservices.nhs.uk/STU3/Patient/6105551233&purpose=PLAN

**Responses**

Where a record does not exist:

- HTTP 200-Request was successfully executed
- Bundle resource of type *searchset* containing a total value of 0 Consent resources.

This would indicate it is safe to create a Consent record for this patient. See [section 2](#section2) for register interaction. 

Example below demonstrates a response where no record exists 

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

Where a record does exist:

- HTTP 200-Request was successfully executed
- Bundle resource of type *searchset* containing a total value of 1 or 2 Consent records, which would contain the unique logical id for each record.
- The existence of a record requires an update interaction to overwrite the existing old record with a new version. The previous version will become historic. See [section 3](#section3) for updating an existing consent record using logical id.

Example of bundle section containing searchset. Note that <id> here is the **bundle id** and **NOT** the consent id:

```xml
<Bundle xmlns="http://hl7.org/fhir">
	<id value="dd9724d1-7b61-44e2-9023-b72e6b966018"/>
	<meta>
		<versionId value="1c268b27-fcd9-45fc-92f7-3781b63c2593"/>
		<lastUpdated value="2017-11-16T11:23:06.269+00:00"/>
	</meta>
	<type value="searchset"/>
	<total value="1"/>**
	<link>
		<relation value="self"/>
		<url value="http://fhir.nhs.uk/Consent?patient=https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234&amp;_format=xml"/>
	</link>
```

<a id="section1"></a>

The remaining section of the same XML contains the Consent record for the patient. The `<id>` here is the unique logical id for the consent record:

```xml

	<entry>
		<fullUrl value="https://fhir.nhs.uk/Consent/0353e505-f7be-4c20-8f4e-337e79a32c51"/>
		<resource>
			<Consent>
				<id value="0353e505-f7be-4c20-8f4e-337e79a32c51"/>
				<meta>
					<versionId value="d837bf2c-dc47-4cb9-9483-03986c21e38c"/>
					<lastUpdated value="2017-11-16T11:17:32.511+00:00"/>
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
				<category>
					<coding>
						<system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-Categories-1"/>
						<code value="NDOP"/>
					</coding>
				</category>
				<patient>
					<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
				</patient>
				<dateTime value="2017-02-01T11:15:33+00:00"/>
				<actor>
					<role>
						<coding>
							<system value="http://hl7.org/fhir/v3/ParticipationType"/>
							<code value="INF"/>
						</coding>
					</role>
					<reference>
						<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
					</reference>
				</actor>
				<organization>
					<reference value="https://directory.spineservices.nhs.uk/STU3/Organization/X26"/>
				</organization>
				<policy>
					<authority value="https://www.gov.uk/"/>
					<uri value="https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.PDF"/>
				</policy>
				<purpose>
					<system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1"/>
					<code value="PLAN"/>
					<display value="Opted out of Planning and Commisioning Data Sharing"/>
				</purpose>
			</Consent>
		</resource>
		<search>
			<mode value="match"/>
		</search>
	</entry>
</Bundle>
```

<a name="section2"></a>

## 2. Register Patients National Data Opt-out Preferences Interaction ##

Where an existing Consent record does not exist, the client system will construct an XML body containing NDOP preferences and submit this to the Spine using a RESTful create interaction.

- ***Sender:*** Any NDOP client
- ***Receiver:*** Spine 2
- ***RESTful API Interaction:*** POST https://fhir.nhs.uk/Consent


{% include note.html content="Details on the FHIR RESTful specification for creating a new instance can be found here [RESTful Create](https://www.hl7.org/fhir/http.html#create)" %}

An example of a new record is displayed below:

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
	<category>
		<coding>
			<system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-Categories-1"/>
			<code value="NDOP"/>
		</coding>
	</category>
	<patient>
		<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
	</patient>
	<dateTime value="2017-11-16T15:17:33+00:00"/>
	<actor>
		<role>
			<coding>
				<system value="http://hl7.org/fhir/v3/ParticipationType"/>
				<code value="INF"/>
			</coding>
		</role>
		<reference>
			<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
		</reference>
	</actor>
	<organization>
		<reference value="https://directory.spineservices.nhs.uk/STU3/Organization/X26"/>
	</organization>
	<policy>
		<authority value="https://www.gov.uk/"/>
		<uri value="https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.PDF"/>
	</policy>
	<purpose>
		<system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1"/>
		<code value="PLAN"/>
		<display value="Opted out of Planning and Commisioning Data Sharing"/>
	</purpose>
</Consent>
```

---
**Responses**

Assuming successful URL submission, there are several possible responses to the NDOP request:

- HTTP 201-Record Created: The entry has been successfully created and the NDOP returns an HTTP Location header containing the 'server' assigned logical Id of the created resource.
- HTTP 400-Bad Request: Resource could not be parsed or failed basic FHIR validation rules
- HTTP 422-Unprocessable Entity: The proposed resource violated applicable FHIR profiles or server business rules.

<a name="section3"></a>

## 3. Update Patients Existing National Data Opt-out Preferences Interaction ##

Where an existing Consent record exists, the client system will perform a RESTful update interaction to amend the patients National Data Opt-out preferences and submit a revised body to the NDOP service. The [logical id](#section1) from the searchset result in section 1 is used in the REST statement, to identify the patient record to be updated and MUST be included in the updated XML body.

- ***Sender:***Any NDOP Client
- ***Receiver:***Spine 2
- ***RESTful API Interaction:***PUT https://[fhir.nhs.uk]/Consent/[logical id] 

The entire XML body will be replaced with a new version to include one or more changes, in addition to the <id> element. Unchanged data MUST still be included.

Example of updated Consent record body from [section 1](#section1). Only status has changed from active to inactive. All other data remains unchanged.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Consent xmlns="http://hl7.org/fhir">
	<id value="0353e505-f7be-4c20-8f4e-337e79a32c51"/>
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
	<category>
		<coding>
			<system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-Categories-1"/>
			<code value="NDOP"/>
		</coding>
	</category>
	<patient>
		<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
	</patient>
	<dateTime value="2017-02-01T11:15:33+00:00"/>
	<actor>
		<role>
			<coding>
				<system value="http://hl7.org/fhir/v3/ParticipationType"/>
				<code value="INF"/>
			</coding>
		</role>
		<reference>
			<reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/6105551234"/>
		</reference>
	</actor>
	<organization>
		<reference value="https://directory.spineservices.nhs.uk/STU3/Organization/X26"/>
	</organization>
	<policy>
		<authority value="https://www.gov.uk/"/>
		<uri value="https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.PDF"/>
	</policy>
	<purpose>
		<system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-PreferenceCodes-1"/>
		<code value="PLAN"/>
		<display value="Opted out of Planning and Commisioning Data Sharing"/>
	</purpose>
</Consent>
```

{% include note.html content="Details on the FHIR RESTful specification for creating a new instance can be found here [RESTful Update](https://www.hl7.org/fhir/http.html#update)" %}

**Responses**

Assuming successful URL submission, there are several possible responses to the NDOP request:

- HTTP 200-OK: The entry has been successfully updated and the NDOP returns an HTTP Location header containing the 'server' assigned logical Id of the updated resource.
- HTTP 400-Bad Request: Resource could not be parsed or failed basic FHIR validation rules
- HTTP 422-Unprocessable Entity: The proposed resource violated applicable FHIR profiles or server business rules.


## 4. Retrieve Patients National Data Opt-out Preferences Interaction ##

The client system performs a RESTful search interaction for current patient preferences located on the National Data Opt-out service.

- ***Sender:***Any NDOP Client
- ***Receiver:***Spine 2
- ***RESTful API Interaction:***GET https://[fhir.nhs.uk]/Consent[parameters] 


{% include note.html content="Details on the FHIR RESTful specification for reading an instance can be found here [RESTful Read](https://www.hl7.org/fhir/http.html#read)" %}
---
**Responses**

The search results **MAY** return one, two or no instances of the patients National Data Opt-out preferences, depending on search parameters. Any instance that is returned **SHALL** have one of the following preferences:

- RESCH - Research Opt-Out
- PLAN - Planning and Commissioning Opt-Out

Assuming successful URL submission, there is one possible outcome to a search request:

- HTTP 200-Request was successfully executed

The NDOP FHIR server determines which of the set of resources it serves meet the specific criteria, and returns the results of the search in the HTTP response as a 'searchset' bundle or as single consent resource.

Note: Although an HTTP response 200 OK indicates the request was successful, the bundle could return a 0 (zero) total value indicating no records were found. An XML example of a Bundle with a 0 (zero) total value indicating no record was found is shown below.

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

