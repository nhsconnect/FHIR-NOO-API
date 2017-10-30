---
title: actorperson extension
keywords: source, extension
tags: [source,extension]
sidebar: profiles_sidebar
permalink: consent_extension_actorperson.html
summary: "low level details for the care connect patient 'SourceOfOptOut' extension"
---

### Element Usage ###

The ActorPerson extension is used to capture an actor that acts on behalf of the patient. This could be a parent defining their childs preferences at a GP practice. In this scenario the patient is the child, the actor is the GP and the parent is the ActorPerson.
 
### SourceOfOptOut ###

|Type|name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
| Extension| Extension-ActorPerson-1| string | Mechanism used to capture an additional actor involved in the defining of preferences.|


**Example of Correct Usage**

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`Extension-NDOP-ActorPerson-1`| Parent of child |Parent asked GP to set preferences for child|

**Example of Incorrect Usage**

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`Extension-NDOP-ActorPerson-1`|GP|GP would be the actor not the ActorPerson|


On the wire XML example

```xml
<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-ActorPerson-1">
	<valueString value="Parent of child"/>
</extension>
```

On the wire example in JSON

```json
{
  "extension": [
	{
    "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-ActorPerson-1",
    "valueString": "Parent of child"
	}
  ]
}
```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.






