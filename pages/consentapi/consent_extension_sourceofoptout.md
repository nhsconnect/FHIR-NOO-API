---
title: sourceofoptout extension
keywords: source, extension
tags: [source,extension]
sidebar: profiles_sidebar
permalink: consent_extension_sourceofoptout.html
summary: "low level details for the care connect patient 'SourceOfOptOut' extension"
---

### Element Usage ###

The SourceOfOptOut extension is used to capture the mechanism used to set the patients national opt-out preferences. This extension is used in conjunction with a series of codes stored within a valueset. 

### SourceOfOptOut ###

|Type|name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
| Extension| Extension-SourceOfOptOut-1| Coding | Mechanism used to capture patient national opt-out preferences |

## Valueset 

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
|![Tick](images/tick.png)|`Extension-SourceOfOptOut-1`| OP |Online Process.|

**Example of Incorrect Usage**

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)||`Extension-SourceOfOptOut-1`|NHS Choices|This is not a value defined within the valueset.|


On the wire XML example

```xml
<extension url="http://fhir.nhs.net/StructureDefinition/extension-cofe-care-setting-type-1">
	<valueCodeableConcept>
		<coding>
			<system value="https://fhir.nhs.uk/opt-out-source-codesystem-1"/>
			<code value="OP"/>
			<display value="Online Process"/>
		</coding>
	</valueCodeableConcept>
</extension>
```

On the wire example in JSON

```json
{
  "birthDate": { "-value": "1957-01-01" }
}
```

*Error Handling*

The provider system SHALL return an error if:

- The `birthDate` value does not comply with the aforementioned format.
- The `birthDate` value is omitted.
- The `birthDate` value is an invalid date.






