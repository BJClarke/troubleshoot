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

# 撤銷 TLS 1.0 及 1.1 支援
{: #tlssupportwithdraw}

IBM 將在 2018 年 3 月 1 日撤銷許多雲端產品及服務的 TLS 1.0 和 TLS 1.1 支援。針對撤銷 TLS 1.0 及 1.1 支援的任何 {{site.data.keyword.Bluemix_notm}} 產品或服務，將會繼續支援 TLS 1.2。
{:shortdesc}

## 為什麼進行這項變更？
{: #why}

這是 IBM 對於提供徹底安全且符合業界在安全及資料隱私方面之最佳作法的承諾的一部分。

## 何謂 TLS？
{: #what}

我們使用了 [TLS 通訊協定](https://en.wikipedia.org/wiki/Transport_Layer_Security)來加密透過網路的通訊，以確保傳輸的資料能維持私密。有三個已發行的 TLS 版本：1.0、1.1 及 1.2。所有 HTTPS 連線都會使用 TLS。HTTPS 是確定您與 {{site.data.keyword.Bluemix_notm}} 產品及服務的連線受信任且安全時，主要的方法。某些 {{site.data.keyword.Bluemix_notm}} 產品及服務容許使用 WebSocket Secure (WSS) 通訊協定來進行安全連線，而該通訊協定也使用 TLS。撤銷 TLS 1.0 及 1.1 支援同時涵蓋 HTTPS 和 WSS 連線。

## 我需要採取哪些動作，才能確保我不會受到影響？
{: #impact}

絕大多數對 {{site.data.keyword.Bluemix_notm}} 產品或服務所進行的連線已使用 TLS 1.2。如果您的連線不需要 TLS 1.0 或 1.1，則您不會受到影響。 

如果您使用任何即將撤銷 TLS 1.0 或 1.1 支援的產品或服務，則必須確認您的連線不需要 TLS 1.0 或 1.1。

### {{site.data.keyword.Bluemix_notm}} 上的 Cloud Foundry

針對 Cloud Foundry 應用程式，您需要確認在下列情況下不會受到影響：從 {{site.data.keyword.Bluemix_notm}} 外連接至應用程式，或是從應用程式連接至 IBM Cloud 上的另一個 Cloud Foundry 應用程式。

所有使用 TLS 的 Cloud Foundry 連線都可能受到影響，包括任何從 Web 瀏覽器建立的連線。所有現代瀏覽器都支援 TLS 1.2，包括作為 [{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/overview/prereqs.html#browsers) 必要條件的瀏覽器。
{: tip}

#### 連接至 Cloud Foundry 應用程式

`*.mybluemix.net` 網域上的所有 Cloud Foundry 應用程式端點，都可以透過只支援 TLS 1.2 的替代端點進行存取。 

若要使用替代端點，請在應用程式子網域的後面新增 `alt.`，例如，如果您的應用程式是在 `https://myapplication.mybluemix.net` 進行管理，則請使用 `https://myapplication.alt.mybluemix.net`。或者，針對 `https://myaplication.eu-gb.mybluemix.net`，使用 `https://myapplication.alt.eu-gb.mybluemix.net`。

如果您能夠順利連接至替代端點，將不會受到影響。 

如果您無法順利連接，則會受到影響，而且必須變更用戶端、用戶端程式庫或用戶端配置，以啟用 TLS 1.2。

#### Cloud Foundry 應用程式之間的連線

使用下列指令，即可將 Cloud Foundry 應用程式配置為在連接至其他應用程式時，自動重新導向至 `*.mybluemix.net` 網域上可用的替代端點：
```
cf <application_name> BLUEMIX_TLS10_DISABLED true
```

將 `BLUEMIX_TLS10_DISABLED` 設為 `true` 之後，必須使用下列指令來重新編譯打包您的應用程式，這項變更才會生效：
```
cf restage <application_name>
```

在您進行這些變更之後，來自應用程式的任何出埠要求都會重新導向至僅限 TLS 1.2 的替代端點。

若要使用替代端點，您的用戶端必須支援「伺服器名稱指示 (SNI)」TLS 延伸規格。否則，您的用戶端可能會將傳回的憑證視為無效。如果發生此情況，您可能會不正確地假設您受到 TLS 1.0 及 1.1 移除作業的影響。
{: tip}

### Watson 產品及服務

針對使用 `gateway.watsonplatform.net` 或 `stream.wastonplatform.net` 所連接的 Watson 產品及服務，請將這個項目取代為 `gateway-tls12.watsonplatform.net` 或 `stream-tls12.watsonplatform.net`。這些替代端點僅支援 TLS 1.2。如果您能夠順利連接至這些端點，則不會受到影響。如果您無法順利連接，則會受到影響，而且必須變更用戶端、用戶端程式庫或用戶端配置，以啟用 TLS 1.2。

未提供非美國南部地區中 Watson 產品及服務的替代端點，因為這些端點僅支援 TLS 1.2。

`gatway-tls12.watsonplatform.net` 及 `stream-tls12.watsonplatform.net` 僅供測試之用，而且在移除 TLS 1.0 及 1.1 之後就無法使用。
{: tip}

### 其他產品或服務

針對沒有可用僅限 TLS 1.2 替代端點的產品或服務，請參閱用戶端或用戶端程式庫的任何可用文件，以取得如何判定所支援 TLS 版本以及所使用版本的相關資訊。

## 撤銷 TLS 1.0 及 1.1 支援的產品及服務為何？
{: #prodsandservs}

下列產品或服務將撤銷對 TLS 1.0 及 1.1 的支援。

多個地區可能會提供部分產品或服務（例如 {{site.data.keyword.Bluemix_notm}} 上的 Cloud Foundry 及 {{site.data.keyword.Bluemix_notm}} 型錄中的服務）。將在目前支援的所有地區中移除 TLS 1.0 及 1.1。

**重要注意事項：**「{{site.data.keyword.Bluemix_notm}} 專用」或「{{site.data.keyword.Bluemix_notm}} 本端系統」部署或者這些部署中所管理的任何 {{site.data.keyword.Bluemix_notm}} 服務不在此列。如果您的部署仍然支援 TLS 1.0 或 1.1，請與客戶或支援代表合作，決定適合移除的時機。

### 可從 IBM Cloud 型錄取得的產品或服務

#### 雲端平台

* {{site.data.keyword.Bluemix_notm}} 上的 Cloud Foundry
* {{site.data.keyword.Bluemix_notm}} 基礎架構（`api.softlayer.com` 及 `api.service.softlayer.com`）

#### API

* API Connect

#### 應用程式服務

* Business Rules
* Message Hub
* Voice Agent with Watson\*
* Watson Content Knowlege Kits\*

#### 資料及分析

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

#### 金融

* Historical Instrument Analytics\*
* Instrument Analytics\*
* Investment Portfolio\*
* Portfolio Optimization\*
* Predictive Market Scenarios\*
* Simulated Historical Instrument Analytics\*
* Simulated Instrument Analytics\*

#### 功能

* 功能

#### 整合

* App Connect
* Product Insights
* Secure Gateway
* API Harmony\*

#### 物聯網

* IoT for Electronics

#### 行動

* App ID†
* Mobile Analytics
* Mobile Foundation
* Push Notifications
* App Launch\*

#### 安全

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

\* 在 {{site.data.keyword.Bluemix_notm}} 型錄的實驗性服務下提供。  
† 已移除 TLS 1.0，只即將移除 TLS 1.1。  
‡ 已淘汰，只有現有客戶才能使用。 

### 可透過 IBM Marketplace 取得的產品或服務

* Forms Experience Builder on Cloud
* IoT for Insurance
* Watson Customer Insight for Insurance
* Watson Marketing Insights
* Watson Knowledge Studio
* Watson Virtual Agent
* Weather Company Energy Trader

### 其他產品或服務

* Teacher Advisor with Watson

## 未列出我的產品或服務時，該怎麼辦？
{: #tlsprodnotlisted}

您的產品或服務可能已經僅支援 TLS 1.2，或者目前不會移除 TLS 1.0 及 1.1。您可以使用各種可用的用戶端及線上工具，來檢查產品或服務的端點是否支援 TLS 1.0 及 1.1。

在 2018 年 1 月 5 日或該日期前，其他產品或服務可能已新增至此公告。

## 在撤銷支援之後，是否有方法可以繼續使用 TLS 1.0 或 1.1？
{: #tlskeepusing}

部分產品及服務會提供替代端點，以在從主要端點移除 TLS 1.0 及 1.1 之後繼續支援 TLS 1.0 及 1.1。

### {{site.data.keyword.Bluemix_notm}} 基礎架構

從支援 TLS 1.0 及 1.1 的 `api.softlayer.com` 及 `api.service.softlayer.com` 中移除 TLS 1.0 及 1.1 支援時，將會公告替代端點並提供使用 30 天。 

### Watson 產品及服務

如果您需要在撤銷支援之後於連接至 Watson 產品及服務時繼續使用 TLS 1.0 或 1.1，可以將 `gateway.watsonplatform.net` 取代為 `gateway-tls10.wastonplatform.net`，或將 `stream.watsonplatform.net` 取代為 `stream-tls10.watsonplatform.net`。`gateway-tls10.watsonplatform.net` 及 `stream-tls10.watsonplatform.net` 支援 TLS 1.0、1.1 及 1.2，而且將在從 `gateway.watsonplatform.net` 及 `stream.watsonplatform.net` 移除 TLS 1.0 及 1.1 之後供您繼續使用。

## 聯繫
{: #tlssupport}

如果您有任何疑問或問題，請與[支援中心](https://www.ibm.com/cloud/support)聯絡。
