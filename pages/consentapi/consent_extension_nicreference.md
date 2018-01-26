---
title: NICReference extension
keywords: NIC, extension, Centre National
tags: [NIC,extension]
sidebar: profiles_sidebar
permalink: consent_extension_nicreference.html
summary: "low level details for the National Data Opt-out 'NICReference' extension"
---

### Element Usage ###

The NICReference extension is used to capture the National Information Centre record reference which is created when a patient or proxy access the contact centre to set preferences.

### NICReference ###

|Type|name|Data Type|Description|
| ------------- | ------------- | ------------- | ------------- |
| Extension| Extension-NDOP-NICReference-1| String | Used to capture National Information Centre record reference |


**Example of Correct Usage**

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`Extension-NDOP-OptOutSource-1`| 1234ABC|

On the wire XML example

```xml
<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-NICReference-1">
	<valueString value="1234ABC"/>
```

On the wire example in JSON

```json
  {
      "fhir_comments": [
        "NIC record reference"
      ],
      "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-NDOP-NICReference-1",
      "valueString": "12345-A"
    }
```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.