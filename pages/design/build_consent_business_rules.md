---
title: Business Rules
keywords: Consent, consentingParty, consentingProxy
tags: [consent,REST,proxy]
sidebar: overview_sidebar
permalink: build_consent_business_rules.html
summary: "Business Rules for National Data Opt-out"
---

## consentingParty and consentingProxyRole Business Rules

The element consentingParty MUST only be populated when the extension consentingProxyRole is omitted from the Consent resource or has a null value. Where the consentingParty is omited or null, the consentingProxyRole element MUST be populated. It is not permitted to include or exclude both elements within the Consent resource.



The grid below provides a visual indicator for acceptable usage

|consentingParty|consentingProxyRole|Permitted|
|Yes|No|![Tick](images/tick.png)|
|No|Yes|![Tick](images/tick.png)|
|Yes|Yes|![Cross](images/cross.png)|
|No|No|![Cross](images/cross.png)|
