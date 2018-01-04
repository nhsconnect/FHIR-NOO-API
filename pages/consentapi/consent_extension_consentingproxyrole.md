---
title: consentingproxyrole extension
keywords: source, extension
tags: [source,extension]
sidebar: profiles_sidebar
permalink: consent_extension_consentingproxyrole.html
summary: "low level details for the consent 'consentingProxyRole' extension"
---

### Element Usage ###

The conseningProxyRole extension is used to capture a patients proxys role that they play whilst setting the patients Opt-out preferences. This could be a parent defining their childs preference at a GP practice or a Court Approved deputy defining an adults preference. 
 
### consentingProxyRole ###

|Type|name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
| Extension| Extension-consentingProxyRole-1| CodeableConcept | Mechanism used to capture a proxy role whilst defining a patients opt-out preference|
|Complex.extension|role|CodeableConcept|The role played by a proxy. Uses https://fhir.nhs.uk/STU3/ValueSet/NDOP-ProxyRole-1|
|Complex.extension|NIC|string|Where a preference was set by a proxy via a contact centre a NIC reference may be provided|


**Example of Correct Usage**

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`Extension-NDOP-consentingProxyRole-1`| GUARDIAN |Patients legally approved guardian|

**Example of Incorrect Usage**

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`Extension-NDOP-consentingProxyRole-1`|GP|GP is not a supported proxy role|


On the wire XML example

```xml
<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-Proxy-1">
				<extension url="role">
			<valueCodeableConcept>
				<coding>
					<system value="https://fhir.nhs.uk/STU3/ValueSet/NDOP-ProxyRole-1"/>
					<code value="POA"/>
					<display value="Power of Attorney"/>
				</coding>
			</valueCodeableConcept>
		</extension>
		<extension url="NIC">
		<valueString value="12345-C"/>
		</extension>
	</extension>
```

On the wire example in JSON

```json
{
      "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-Proxy-1",
      "extension": [
        {
          "url": "role",
          "valueCodeableConcept": {
            "coding": [
              {
                "system": "https://fhir.nhs.uk/STU3/ValueSet/NDOP-ProxyRole-1",
                "code": "POA",
                "display": "Power of Attorney"
              }
            ]
          }
}
```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.






