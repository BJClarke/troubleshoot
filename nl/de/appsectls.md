---

copyright:

  years: 1994, 2017

lastupdated: "2017-11-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}

# Unterstützung für TLS 1.0 und 1.1 wird eingestellt
{: #tlssupportwithdraw}

IBM stellt die Unterstützung für TLS 1.0 und TLS 1.1 bei vielen Cloud-Produkten und -Services von IBM am 1. März 2018 ein. TLS 1.2 wird weiterhin für alle {{site.data.keyword.Bluemix_notm}}-Produkte und -Services unterstützt, bei denen die Unterstützung für TLS 1.0 und 1.1 eingestellt wird.
{:shortdesc}

## Was ist der Grund für diesen Wechsel? 
{: #why}

Diese Maßnahme erfolgt im Rahmen der Bestrebungen von IBM, eine Cloud bereitzustellen, die profunde Sicherheit bietet und an den Best Practices der Branche in Bezug auf Sicherheit und Datenschutz ausgerichtet ist. 

## Was ist TLS?
{: #what}

Das [TLS-Protokoll](https://en.wikipedia.org/wiki/Transport_Layer_Security) wird zur Verschlüsselung der Kommunikation innerhalb eines Netzes verwendet, um sicherzustellen, dass die übertragenen Daten vor unbefugten Zugriffen geschützt sind. Es gibt drei freigegebene TLS-Versionen: 1.0, 1.1 und 1.2. Bei allen HTTPS-Verbindungen wird TLS verwendet. Im Allgemeinen wird mithilfe von HTTPS sichergestellt, dass Ihre Verbindungen zu {{site.data.keyword.Bluemix_notm}}-Produkten und -Services zuverlässig und sicher sind. Einige {{site.data.keyword.Bluemix_notm}}-Produkte und -Service ermöglichen sichere Verbindungen über das WSS-Protokoll (WSS = WebSocket Secure), bei dem ebenfalls TLS verwendet wird. Das Einstellen der Unterstützung für TLS 1.0 und 1.1 bezieht sich sowohl auf HTTPS- als auch auf WSS-Verbindungen. 

## Welche Vorkehrungen muss ich treffen, um Beeinträchtigungen zu vermeiden? 
{: #impact}

Bei der überwiegenden Mehrzahl der Verbindungen zu {{site.data.keyword.Bluemix_notm}}-Produkten und -Services wird bereits TLS 1.2 verwendet. Wenn Ihre Verbindungen TLS 1.0 oder 1.1 nicht erfordern, beinhaltet das Einstellen der Unterstützung keine Beeinträchtigungen für Sie.  

Wenn Sie Produkte oder Services verwenden, bei denen die Unterstützung für TLS 1.0 oder 1.1 eingestellt wird, müssen Sie sich vergewissern, dass Ihre Verbindungen TLS 1.0 oder 1.1 nicht benötigen. 

### Cloud Foundry in {{site.data.keyword.Bluemix_notm}}

Bei Cloud Foundry-Anwendungen müssen Sie sich vergewissern, dass das Einstellen der Unterstützung keine Auswirkungen hat, wenn Sie außerhalb von {{site.data.keyword.Bluemix_notm}} Verbindungen zu Ihrer Anwendung herstellen oder von Ihrer Anwendung aus Verbindungen zu einer anderen Cloud Foundry-Anwendung in IBM Cloud hergestellt werden. 

Alle Verbindungen zu Cloud Foundry, bei denen TLS verwendet wird, sind möglicherweise betroffen. Dies schließt über Web-Browser hergestellte Verbindungen ein. Alle aktuellen Browser, die für [{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/overview/prereqs.html#browsers) vorausgesetzten Browser eingeschlossen, unterstützen TLS 1.2.
{: tip}

#### Verbindung zu Ihrer Cloud Foundry-Anwendung herstellen

Auf alle Cloud Foundry-Anwendungsendpunkte in der Domäne `*.mybluemix.net` kann über einen alternativen Endpunkt zugegriffen werden, der ausschließlich TLS 1.2 unterstützt.  

Fügen Sie zum Verwenden dieses alternativen Endpunkts `alt.` im Anschluss an den Namen der Unterdomäne Ihrer Anwendung ein. Wenn Ihre Anwendung beispielsweise unter `https://myapplication.mybluemix.net` gehostet wird, verwenden Sie `https://myapplication.alt.mybluemix.net`. Ein weiteres Beispiel ist die Verwendung von `https://myaplication.alt.eu-gb.mybluemix.net` anstelle von `https://myapplication.eu-gb.mybluemix.net`. 

Kann die Verbindung zu dem alternativen Endpunkt hergestellt werden, beinhaltet das Einstellen der Unterstützung keine Beeinträchtigungen für Sie.  

Kann die Verbindung nicht erfolgreich hergestellt werden, stehen Beeinträchtigungen an. Sie müssen in diesem Fall Ihren Client, die Clientbibliotheken oder die Clientkonfiguration ändern, um TLS 1.2 zu aktivieren. 

#### Verbindungen zwischen Cloud Foundry-Anwendungen

Sie können Ihre Cloud Foundry-Anwendung mit dem folgenden Befehl so konfigurieren, dass beim Herstellen von Verbindungen zu anderen Anwendungen automatisch eine Weiterleitung an die in der Domäne `*.mybluemix.net` verfügbaren alternativen Endpunkte erfolgt: 
```
cf <Anwendungsname> BLUEMIX_TLS10_DISABLED true
```

Nachdem Sie für `BLUEMIX_TLS10_DISABLED` den Wert `true` festgelegt haben, muss mit dem folgenden Befehl ein erneutes Staging für die Anwendung durchgeführt werden, damit die Änderung wirksam wird: 
```
cf restage <Anwendungsname>
```

Nach diesen Änderungen werden abgehende Anforderungen Ihrer Anwendung an die alternativen Endpunkte weitergeleitet, bei denen ausschließlich TLS 1.2 verwendet wird. 

Ihr Client muss die TLS-Erweiterung SNI (Server Name Indication) unterstützen, damit die alternativen Endpunkte verwendet werden können. Wird SNI nicht unterstützt, werden die zurückgegebenen Zertifikate möglicherweise von Ihrem Client als ungültig bewertet. Wenn dies der Fall ist, führt Sie dies möglicherweise zu der Fehleinschätzung, dass das Einstellen der Unterstützung für TLS 1.0 und 1.1 Beeinträchtigungen für Sie beinhaltet.
{: tip}

### Watson-Produkte und -Services

Bei Watson-Produkten und -Services, zu denen Sie mit `gateway.watsonplatform.net` oder `stream.wastonplatform.net` eine Verbindung herstellen, müssen Sie stattdessen `gateway-tls12.watsonplatform.net` oder `stream-tls12.watsonplatform.net` verwenden. Diese alternativen Endpunkte unterstützen ausschließlich TLS 1.2. Kann eine Verbindung zu diesen alternativen Endpunkten hergestellt werden, beinhaltet das Einstellen der Unterstützung keine Beeinträchtigungen für Sie. Kann die Verbindung nicht erfolgreich hergestellt werden, stehen Beeinträchtigungen an. Sie müssen in diesem Fall Ihren Client, die Clientbibliotheken oder die Clientkonfiguration ändern, um TLS 1.2 zu aktivieren. 

In anderen Regionen als der Region 'Vereinigte Staaten (Süden)' werden keine alternativen Endpunkte für Watson-Produkte und -Services bereitgestellt, da in diesen Regionen bereits ausschließlich TLS 1.2 unterstützt wird. 

`gateway-tls12.watsonplatform.net` und `stream-tls12.watsonplatform.net` sind nur für Testzwecke vorgesehen und nach dem Einstellen der Unterstützung von TLS 1.0 und 1.1 nicht mehr verfügbar.
{: tip}

### Sonstige Produkte und Services

Finden Sie bei Produkten und Services, für die keine alternativen Endpunkte, die ausschließlich TLS 1.2 unterstützen, verfügbar sind, anhand der für Ihren Client oder Ihre Clientbibliothek verfügbaren Dokumentation heraus, welche TLS-Versionen unterstützt werden und welche Version von Ihnen verwendet wird. 

## Bei welchen Produkten und Services wird die Unterstützung für TLS 1.0 und 1.1 eingestellt? 
{: #prodsandservs}

Bei den im Folgenden aufgeführten Produkten und Services wird die Unterstützung für TLS 1.0 und 1.1 eingestellt. 

Einige Produkte und Services, z. B. Cloud Foundry in {{site.data.keyword.Bluemix_notm}} und Services im {{site.data.keyword.Bluemix_notm}}-Katalog, werden möglicherweise in mehreren Regionen angeboten. Die Unterstützung für TLS 1.0 und 1.1 wird in allen Regionen entfernt, in denen diese Protokollversionen zurzeit unterstützt werden. 

**Wichtig: ** {{site.data.keyword.Bluemix_notm}} Private und {{site.data.keyword.Bluemix_notm}} Local System-Bereitstellungen sowie in diesen Bereitstellungen gehostete {{site.data.keyword.Bluemix_notm}}-Services sind nicht eingeschlossen. Wenn Ihre Bereitstellung weiterhin TLS 1.0 oder 1.1 unterstützt, wenden Sie sich an Ihren Ansprechpartner beim Kundendienst und klären Sie mit ihm, wann diese Unterstützung beendet werden sollte. 

### Über den IBM Cloud-Katalog verfügbare Produkte und Services

#### Cloudplattform

* Cloud Foundry in {{site.data.keyword.Bluemix_notm}}
* {{site.data.keyword.Bluemix_notm}}-Infrastruktur (`api.softlayer.com` und `api.service.softlayer.com`)

#### APIs

* API Connect

#### Application Services

* Business Rules
* Message Hub
* Voice Agent with Watson\*
* Watson Content Knowledge Kits\*

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
* Verwalteter MS SQL-Datenbankserver\*

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

#### Finanzen

* Historical Instrument Analytics\*
* Instrument Analytics\*
* Investment Portfolio\*
* Portfolio Optimization\*
* Predictive Market Scenarios\*
* Simulated Historical Instrument Analytics\*
* Simulated Instrument Analytics\*

#### Funktionen

* Funktionen

#### Integration

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

#### Sicherheit

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

\* Bei experimentellen Services im {{site.data.keyword.Bluemix_notm}}-Katalog verfügbar.   
† TLS 1.0 wurde bereits entfernt, lediglich das Einstellen der Unterstützung für TLS 1.1 ist noch nicht vollständig vollzogen.   
‡ Wird nicht weiter unterstützt. Nur noch verfügbar für Bestandskunden.  

### Über IBM Marketplace verfügbare Produkte und Services

* Forms Experience Builder on Cloud
* IoT for Insurance
* Watson Customer Insight for Insurance
* Watson Marketing Insights
* Watson Knowledge Studio
* Watson Virtual Agent
* Weather Company Energy Trader

### Sonstige Produkte und Services

* Teacher Advisor with Watson

## Was ist, wenn mein Produkt bzw. Service nicht in der Liste enthalten ist? 
{: #tlsprodnotlisted}

Möglicherweise unterstützt Ihr Produkt bzw. Service bereits ausschließlich TLS 1.2 oder die Unterstützung für TLS 1.0 und 1.1 wird noch nicht eingestellt. Sie können mit verschiedenen Client- und Online-Tools überprüfen, ob TLS 1.0 und 1.1 von den Endpunkten eines Produkts oder Service unterstützt werden. 

Zu der vorliegenden Mitteilung können bis zum 5. Januar 2018 weitere Produkte oder Services hinzugefügt werden. 

## Kann ich TLS 1.0 oder 1.1 nach dem Einstellen der Unterstützung weiterhin verwenden?
{: #tlskeepusing}

Einige Produkte und Services stellen alternative Endpunkte zur Verfügung, bei denen TLS 1.0 und 1.1 auch nach dem Entfernen von TLS 1.0 und 1.1 auf den primären Endpunkten weiter unterstützt werden. 

### {{site.data.keyword.Bluemix_notm}}-Infrastruktur

Wenn die Unterstützung für TLS 1.0 und 1.1 bei `api.softlayer.com` und `api.service.softlayer.com` entfernt wird, werden alternative Endpunkte, die TLS 1.0 und 1.1 unterstützen, angekündigt und 30 Tage zur Verfügung gestellt.  

### Watson-Produkte und -Services

Wenn Sie TLS 1.0 oder 1.1 bei Verbindungen zu Watson-Produkten und -Services auch nach dem Einstellen der Unterstützung weiterhin verwenden müssen, können Sie `gateway.watsonplatform.net` durch `gateway-tls10.wastonplatform.net` oder `stream.watsonplatform.net` durch `stream-tls10.watsonplatform.net` ersetzen. `gateway-tls10.watsonplatform.net` und `stream-tls10.watsonplatform.net` unterstützen TLS 1.0, 1.1 und 1.2 und stehen Ihnen auch nach dem Entfernen von TLS 1.0 und 1.1 bei `gateway.watsonplatform.net` und `stream.watsonplatform.net` weiterhin zur Verfügung. 

## Kontaktaufnahme
{: #tlssupport}

Fordern Sie bei Fragen, Bedenken oder Problemen [Unterstützung](https://www.ibm.com/cloud/support) an. 
