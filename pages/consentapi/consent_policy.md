---
title: policy Element
keywords: policy, consent
tags: [profile,element,policy]
sidebar: overview_sidebar
permalink: consent_policy.html
summary: "low level details for the National Opt-Out 'policy' element"
---
### Element Usage ###

The policy element is used to store the policy to which the consent is based upon. This should be a resolvable uri, that may be accessed to display the full details of the policy. 
 
### policy ###

|Name|Data Type|Description|
| ------------- | ------------- | ------------- |
| policy| url | url that links to the policy which the consent relates to.|


**Example of Correct Usage**

|Usage| Element| examples| Comments|
|![Tick](images/tick.png)|`policy`| https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.PDF |Resolvable link to a PDF document that contains the details of the policy.|

**Example of Incorrect Usage**

|Usage| Element| examples| Comments|
|![Cross](images/cross.png)|`policy`|https://www.gov.uk|Does not direct to a specific policy document.|


On the wire XML example

```xml
    <policy>
		<authority value="https://www.gov.uk/"/>
		<uri value="https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.PDF"/>
    </policy>
```

On the wire example in JSON

```json
{
  "policy": [
	{
	"authority": "https://www.gov.uk/",
    "url": "https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.PDF"
	}
  ]
}
```

*Error Handling*

HTTP response codes will determine the success or failure of the POST operation. No element specific codes will be generated upon failure to POST.




