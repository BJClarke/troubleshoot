---

copyright:

  years: 1994, 2018

lastupdated: "2018-01-05"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Withdrawal of support for TLS 1.0 and 1.1
{: #tlssupportwithdraw}

IBM will withdraw support for TLS 1.0 and TLS 1.1 across many cloud products and services on 01 March 2018. TLS 1.2 will continue to be supported for any {{site.data.keyword.Bluemix_notm}} product or service that is withdrawing support for TLS 1.0 and 1.1.
{:shortdesc}

## Why are we making this change?
{: #why}

This is part of IBM's commitment to offering a cloud that is secure to the core and in alignment with industry best practices for security and data privacy.

## What is TLS?
{: #what}

The [TLS protocol](https://en.wikipedia.org/wiki/Transport_Layer_Security) is used to encrypt communications across a network to ensure that transmitted data remains private. There are three released versions of TLS: 1.0, 1.1, and 1.2. All HTTPS connections use TLS. HTTPS is the predominant method of ensuring that your connections to {{site.data.keyword.Bluemix_notm}} products and services are trusted and secure. Some {{site.data.keyword.Bluemix_notm}} products and services allow secure connections using the WebSocket Secure (WSS) protocol which also uses TLS. Withdrawal of support for TLS 1.0 and 1.1 covers both HTTPS and WSS connections.

## What actions do I need to take to make sure I will not be impacted?
{: #impact}

A significant majority of connections made to {{site.data.keyword.Bluemix_notm}} products or services already use TLS 1.2. If your connections do not require TLS 1.0 or 1.1 you will not be impacted.

If you are using any of the products of services that are withdrawing support for TLS 1.0 or 1.1 you must confirm that your connections do not require TLS 1.0 or 1.1.

### Cloud Foundry on {{site.data.keyword.Bluemix_notm}}

For Cloud Foundry applications you need to confirm that you will not not be impacted when connecting to your application from outside of {{site.data.keyword.Bluemix_notm}} or when connecting from your application to another Cloud Foundry application on IBM Cloud.

All connections to Cloud Foundry that use TLS are potentially impacted, including any connections made from web browsers. All modern browsers support TLS 1.2, including those that are prerequisites for [{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/overview/prereqs.html#browsers).
{: tip}

#### Connecting to your Cloud Foundry application

All Cloud Foundry application endpoints on the `*.mybluemix.net` domain can be accessed through an alternate endpoint that supports only TLS 1.2.

To use the alternate endpoint add `alt.` after your application’s subdomain, for example, if your application is hosted at `https://myapplication.mybluemix.net` use `https://myapplication.alt.mybluemix.net`. Or, for `https://myaplication.eu-gb.mybluemix.net` use `https://myapplication.alt.eu-gb.mybluemix.net`.

If you are able to successfully connect to the alternate endpoint you will not be impacted.

If you cannot successfully connect, you will be impacted and must change your client, client libraries, or client configuration to enable TLS 1.2.

#### Connecting between Cloud Foundry applications

You can configure your Cloud Foundry application to automatically redirect to the alternate endpoints available on the `*.mybluemix.net` domain when connecting to other applications by using the following command:
```
cf <application_name> BLUEMIX_TLS10_DISABLED true
```

After you set `BLUEMIX_TLS10_DISABLED` to `true` your application must be restaged by using the following command for this change to take effect:
```
cf restage <application_name>
```

After you make these changes, any outbound request from your application will redirect to the alternate TLS 1.2-only endpoints.

To use the alternate endpoints, your client must support the Server Name Indication (SNI) TLS extension. If it does not, the returned certificate might be considered invalid by your client. If this occurs, you might incorrectly assume that you are impacted by TLS 1.0 and 1.1 removal.
{: tip}

### Watson products and services

For Watson products and services that you connect to using `gateway.watsonplatform.net` or `stream.wastonplatform.net` replace thise with `gateway-tls12.watsonplatform.net` or `stream-tls12.watsonplatform.net`. These alternate endpoints support TLS 1.2 only. If you are able to successfully connect to these, you will not be impacted. If you cannot successfully connect you will be impacted and must change your client, client libraries, or client configuration to enable TLS 1.2.

Alternate endpoints for Watson products and services in regions other than US South are not provided as these already support only TLS 1.2.

`gatway-tls12.watsonplatform.net` and `stream-tls12.watsonplatform.net` are for testing purposes only and will not be available after TLS 1.0 and 1.1 are removed.
{: tip}

### Other products or services

For products or services that do not have alternate TLS 1.2-only endpoints available refer to any available documentation for your client or client libraries for information on how to determine which versions of TLS are supported and which version you are using.

## What products and services are withdrawing support for TLS 1.0 and 1.1?
{: #prodsandservs}

The following products or services are withdrawing support for TLS 1.0 and 1.1.

Some products or services, such as Cloud Foundry on {{site.data.keyword.Bluemix_notm}} and services in the {{site.data.keyword.Bluemix_notm}} catalog, might be offered in multiple regions. TLS 1.0 and 1.1 will be removed across all regions where they are currently supported.

**Important note:** {{site.data.keyword.Bluemix_notm}} Private or {{site.data.keyword.Bluemix_notm}} Local System deployments or any {{site.data.keyword.Bluemix_notm}} services hosted in these deployments are not included. If your deployment still supports TLS 1.0 or 1.1, work with your customer or support representative to determine when removal is right for you.

### Products or services available from the IBM Cloud catalog

#### Cloud Platform

* Cloud Foundry on {{site.data.keyword.Bluemix_notm}}
* {{site.data.keyword.Bluemix_notm}} infrastructure (`api.softlayer.com` and `api.service.softlayer.com`)

#### APIs

* API Connect

#### Application Services

* Business Rules
* Message Hub
* Voice Agent with Watson\*
* Watson Content Knowlege Kits\*

#### Data & Analytics

* Compose Enterprise
* Compose for Elasticsearch
* Compose for etcd
* Compose for JanusGraph
* Compose for MongoDB
* Compose for MySQL
* Compose for PostgreSQL
* Compose for RabbitMQ
* Compose for Redis
* Compose for RethinkDB
* Compose for ScyllaDB
* Data Catalog
* Data Connect
* Data Refinery
* Decision Optimization
* Graph
* Informix
* Lift
* Weather Company Data
* Managed MS-SQL Database Server\*

#### DevOps

* Auto-Scaling
* Alert Notification
* Availability Monitoring
* Continuous Release
* DevOps Insights
* Event Management
* Globalization Pipeline
* Automated Accessibility Tester\*
* Digital Content Checker\*
* Runbook Automation\*

#### Finance

* Historical Instrument Analytics\*
* Instrument Analytics\*
* Investment Portfolio\*
* Portfolio Optimization\*
* Predictive Market Scenarios\*
* Simulated Historical Instrument Analytics\*
* Simulated Instrument Analytics\*

#### Functions

* Functions

#### Integrate

* App Connect
* Product Insights
* Secure Gateway
* API Harmony\*

#### Internet of Things

* IoT for Electronics

#### Mobile

* App ID†
* Mobile Analytics
* Mobile Foundation
* Push Notifications
* App Launch\*

#### Security

* App ID†
* SSL Certificates†

#### Watson

* Conversation
* Discovery
* Language Translator
* Natural Language Classifier
* Natural Language Understanding
* Personality Insights
* Speech to Text
* Text to Speech
* Tone Analyzer
* Visual Recognition
* Knowledge Studio\*
* Document Conversion‡
* Retrieve & Rank‡
* Tradeoff Analytics‡

\* Available under experimental services in the {{site.data.keyword.Bluemix_notm}} catalog.  
† TLS 1.0 has already been removed, only TLS 1.1 is being removed.  
‡ Deprecated, only available to existing customers.

### Products or services available through IBM Marketplace

* Forms Experience Builder on Cloud
* IoT for Insurance
* Watson Customer Insight for Insurance
* Watson Marketing Insights
* Watson Knowledge Studio
* Watson Virtual Agent
* Weather Company Energy Trader

### Other products or services
{: #prodservices}

* Teacher Advisor with Watson

## What if my product or service isn't listed?
{: #tlsprodnotlisted}

Your product or service might already only support TLS 1.2 or might not be removing TLS 1.0 and 1.1 at this time. There are various client and online tools available that you can use to check whether TLS 1.0 and 1.1 are supported by a product or service's endpoints.

Additional products or services might be added to this announcement on or before 05 January 2018.

## Is there a way I can keep using TLS 1.0 or 1.1 after support is withdrawn?
{: #tlskeepusing}

Some products and services are making alternate endpoints available that will continue to support TLS 1.0 and 1.1 after TLS 1.0 and 1.1 are removed from the primary endpoints.

### {{site.data.keyword.Bluemix_notm}} infrastructure

When support for TLS 1.0 and 1.1 is removed from `api.softlayer.com` and `api.service.softlayer.com` alternate endpoints that support TLS 1.0 and 1.1 will be announced and made available for 30 days.

### Watson products and services
{: #watsonprodservices}

If you need to continue to use TLS 1.0 or 1.1 when connecting to Watson products and services after support is withdrawn you can replace `gateway.watsonplatform.net` with `gateway-tls10.wastonplatform.net` or `stream.watsonplatform.net` with `stream-tls10.watsonplatform.net`. `gateway-tls10.watsonplatform.net` and `stream-tls10.watsonplatform.net` support TLS 1.0, 1.1, and 1.2 and will continue be available for your use after TLS 1.0 and 1.1 are removed from `gateway.watsonplatform.net` and `stream.watsonplatform.net`.

## Get in touch
{: #tlssupport}

If you have any questions, concerns, or problems, contact [support](https://www.ibm.com/cloud/support).
