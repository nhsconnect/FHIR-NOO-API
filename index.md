---
title: Introduction to National Data Opt-out Programme
keywords: ndop, opt-out
tags: [getting_started]
sidebar: overview_sidebar
permalink: index.html
toc: true
summary: A brief introduction to getting started with the National Data Opt-out Programme FHIR&reg; API
---

{% include important.html content="This site is under active development by the interoperability messaging team and is intended to provide all the technical resources you need to successfully deploy a National Data Opt-out Programme Profile. Some areas are being formulated and iterative updates to content will be added on a regular basis." %}

# Background #

The National Data Opt-out Programme (NDOP) is a product of the National Data Guardian (NDG) review on data security and how individuals' data is used and shared by healthcare organizations.  NDOP has been created to provide a model that will allow each individual patient to have control over specific data, being able to choose the purposes for which data can be shared.

NDOP will provide a mechanism for patients registered with a GP in England to control the following data sharing preferences:

- Data for use within Planning and Commissioning
- Data for use within healthcare research


The initial phase will provide an on-line portal where patients can use a standard web browser to set their data sharing preferences. Additional mechanisms will be introduced at a later date, including GP Practice Systems, mobile devices and off-line systems. 

## National Data Opt-out Programme API ##

The National Data Opt-out Programme requires an API to capture the preferences chosen via the online portal and transfer these preferences to a centralized data store located on Spine. The API will use the HL7 FHIR&reg; standard to enable preferences to be created, retrieved and updated using REST methods. A FHIR RESTful API using HTTP request/response, allowing rapid development of applications using the NDOP API.

The NDOP API is relatively lightweight in its design, made up of limited components, making it easy to maintain and deploy.

