---
title: API Codes
keywords: development
tags: [rest,fhir,api]
sidebar: overview_sidebar
permalink: resources_api_codes.html
summary: "Details of the API Codes used in the responses."
---
{% include custom/search.warnbanner.html %}

## 1. API Codes ##

### 1.1. 2xx Http Success ###

#### 200 OK ####
Successful Operation

#### 201 Created ####
The resource was created.

### 1.2. 4xx Http Client Errors ###

#### 405 Method Not Allowed ####

An attempt was made to create a resource using a PUT rather than a POST

**Spine operationOutcome:** MSG_RESOURCE_ID_FAIL - Client is not permitted to assign an id

#### 422 Unprocessable Entity ####

A resource already exists for the patient

**Spine operationOutcome:** DUPLICATE_REJECTED - Create would lead to creation of a duplicate resource
