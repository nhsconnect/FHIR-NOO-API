---
title: sourceofoptout extension
keywords: source, extension
tags: [source,extension]
sidebar: profiles_sidebar
permalink: consent_extension_sourceofoptout.html
summary: "low level details for the care connect patient 'SourceOfOptOut' extension"
---

### Element Usage ###

The SourceOfOptOut extension is used to capture the mechanism used to set the patients National Data Opt-out preferences. Valid codes are taken from the CodeSystem [https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-OptOutSource-1](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-OptOutSource-1).

### SourceOfOptOut ###

|Type|name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
| Extension| Extension-SourceOfOptOut-1| Coding | Mechanism used to capture patient National Data Opt-out preferences |

## CodeSystem 

National Data Opt-out supports the following source of opt-out codes:

|Code|Display|Definition|
|OP|OP|Online Process|
|GP|GP|GP System|
|PFSP|PFSP|Patient Facing Service App|
|FN|FN|Form on NHS.UK|
|CC|CC|Call Centre|
|PP|PP|Paper Process|


**Example of Correct Usage**

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`Extension-NDOP-OptOutSource-1`| OP |Online Process.|

**Example of Incorrect Usage**

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`Extension-NDOP-OptOutSource-1`|NHS Choices|This is not a value defined within the valueset.|


On the wire XML example

```xml
<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-OptOutSource-1">
	<valueCodeableConcept>
		<coding>
			<system value="https://fhir.nhs.uk/STU3/CodeSystem/NDOP-OptOutSource-1"/>
			<code value="OP"/>
			<display value="Online Process"/>
		</coding>
	</valueCodeableConcept>
</extension>
```

On the wire example in JSON

```json
{
  extension: [
	"valuecodeableconcept" : {
	"coding": [
	  {
		"system": "https://fhir.nhs.uk/STU3/CodeSystem/NDOP-OptOutSource-1",
		"code": "OP",
		"display": "Online process"
	  }
   ]
  }
 ]
}

```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.





