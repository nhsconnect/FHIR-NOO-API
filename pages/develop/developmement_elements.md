---
title: Profile Elements
keywords: elements, consent
tags: [profile,elements,usage]
sidebar: overview_sidebar
permalink: development_elements.html
summary: "Implementation guide on the characteristics and usage of the profiles elements"
---
{% include custom/search.warnbanner.html %}

### Consent ###

The Natioanl Data Opt-out API captures a request to create a new Opt-out record or update an existing one if it already exists. 


The following FHIR profiles are used to form the Consent record:

- [NDOP-Consent-1](https://fhir.nhs.uk/STU3/StructureDefinition/NDOP-Consent-1)

### Consent data item mapping to FHIR profiles ###

The consent data item are fulfilled by elements within the FHIR resources listed below:

| EOL Data Item         | FHIR resource element                   			| Mandatory/Required/Optional |Notes																		  				|
|-----------------------|---------------------------------------------------|-----------------------------|---------------------------------------------------------------------------------------------|
| Consent Status        | NDOP-Consent-1.status     	          			| Mandatory                   | Active = Consent Refused, Inactive = Consent Granted.						  				|
| Patient				| NDOP-Consent-1.patient				  			| Mandatory					  | PDS reference to patient             										  				|
| Date/Time 			| NDOP-Consent.dateTime								| Mandatory					  | Date and time when consent record was created.												|
| ConsentingParty		| NDOP-Consent-1.consentingParty 				    | Optional					  | Patient who grants rights to sharing data									  				|
| Organisation			| NDOP-Consent-1.organization						| Mandatory					  | Custodian of the consent.												 	  				|
| Policy				| NDOP-Consent-1.policy					 	        | Mandatory					  | The policy that the consent covers.										      				|
| Purpose				| NDOP-Consent-1.purpose			  	  			| Mandatory					  | An indication as to what the consent permits. SNOMED-CT coded where possible. 				|
| opt-out Source	  	| NDOP-Consent-1.optOutSource (extension) 			| Mandatory    			  	  | Where the Opt-out request originated from.									  				|
| Consenting Proxy Role | NDOP-Consent-1.consentingProxyRole (extension) 	| Optional		  			  | Where the consenting party was not the patient, who was the acting proxy	  				|
| NIC Reference			| NDOP-Consent-1.NICReference (extension) 		    | Optional					  |	National Information Centre reference where this service was used to set Opt-out preference.|

### Consent Example XML ###

<script src="https://gist.github.com/IOPS-DEV/8897e287a007ba61403b1573503fc971.js"></script>

