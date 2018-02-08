---

copyright:

  years: 1994, 2018

lastupdated: "2018-01-09"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# TLS 1.0 および 1.1 のサポート終了
{: #tlssupportwithdraw}

IBM は、2018 年 3 月 1 日付けでクラウド製品ならびにサービスの多くで TLS 1.0 および TLS 1.1 のサポートを終了します。TLS 1.0 および 1.1 のサポートを終了するいずれの {{site.data.keyword.Bluemix_notm}} 製品およびサービスでも、TLS 1.2 は引き続きサポートされます。
{:shortdesc}

## この変更を行う理由
{: #why}

これは、徹底してセキュアなクラウドを提供するための IBM の取り組みの一貫であり、セキュリティーおよびデータ・プライバシーに関する業界のベスト・プラクティスと歩調を合わせるためでもあります。

## TLS とは?
{: #what}

[TLS プロトコル](https://en.wikipedia.org/wiki/Transport_Layer_Security)は、送信データの秘密が守られるようにネットワーク間の通信を暗号化するために使用されます。 リリースされている TLS のバージョンには、1.0、1.1、および 1.2 の 3 つがあります。 HTTPS 接続はすべて TLS を使用します。 HTTPS は、{{site.data.keyword.Bluemix_notm}} 製品およびサービスへの接続がセキュアで信頼できることを保証するための主要な方式です。 一部の {{site.data.keyword.Bluemix_notm}} 製品およびサービスは、WebSocket Secure (WSS) プロトコルを使用したセキュア接続を許可していますが、このプロトコルも TLS を使用します。 TLS 1.0 および 1.1 のサポート終了は、HTTPS 接続と WSS 接続の両方に該当します。

## 影響を受けないようにするには、どのような処置が必要ですか?
{: #impact}

{{site.data.keyword.Bluemix_notm}} 製品またはサービスに対して行われる接続の大部分は既に TLS 1.2 を使用しています。 ご使用の接続が TLS 1.0 または 1.1 を必要としない場合、影響は受けません。

TLS 1.0 または 1.1 のサポートが終了されるいずれかの製品またはサービスを使用している場合、接続が TLS 1.0 または 1.1 を必要としないことを確認する必要があります。

### {{site.data.keyword.Bluemix_notm}} 上の Cloud Foundry

Cloud Foundry アプリケーションに関しては、{{site.data.keyword.Bluemix_notm}} 外部からアプリケーションに接続するとき、またはアプリケーションから IBM Cloud 上の別の Cloud Foundry アプリケーションに接続するときに影響を受けないことを確認しておく必要があります。

Web ブラウザーから行われる接続を含め、Cloud Foundry への TLS を使用するすべての接続は影響を受ける可能性があります。 [{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/overview/prereqs.html#browsers) の前提条件となっているブラウザーを含め、最新のブラウザーはすべて TLS 1.2 をサポートしています。
{: tip}

#### Cloud Foundry アプリケーションへの接続

`*.mybluemix.net` ドメインのすべての Cloud Foundry アプリケーション・エンドポイントに、TLS 1.2 のみをサポートする代替エンドポイントからアクセスできます。

代替エンドポイントを使用するには、アプリケーションのサブドメインの後に `alt.` を追加します。例えば、アプリケーションが `https://myapplication.mybluemix.net` でホストされている場合、`https://myapplication.alt.mybluemix.net` を使用します。 また、`https://myaplication.eu-gb.mybluemix.net` であれば、`https://myapplication.alt.eu-gb.mybluemix.net` を使用します。

代替エンドポイントに正常に接続できる場合、影響を受けることはありません。

正常に接続できない場合は、影響を受けることになるので、クライアント、クライアント・ライブラリー、またはクライアント構成を変更して、TLS 1.2 に対応できるようにする必要があります。

#### Cloud Foundry アプリケーション間の接続

他のアプリケーションに接続するとき、`*.mybluemix.net` ドメイン上の使用可能な代替エンドポイントに自動的にリダイレクトするように Cloud Foundry アプリケーションを構成できます。そうするには以下のコマンドを使用します。
```
cf <application_name> BLUEMIX_TLS10_DISABLED true
```

`BLUEMIX_TLS10_DISABLED` を `true` に設定した後は、この変更を有効にするために以下のコマンドを使用してアプリケーションを再ステージングする必要があります。
```
cf restage <application_name>
```

これらの変更を加えると、アプリケーションからのアウトバウンド要求は代替の TLS 1.2 専用エンドポイントにリダイレクトされます。

代替エンドポイントを使用するには、クライアントがサーバー名表示 (SNI) TLS 拡張機能をサポートしていなければなりません。 サポートしていない場合、返される証明書がクライアントによって無効と見なされる可能性があります。 これが発生すると、TLS 1.0 および 1.1 の廃止による影響であると誤った推測がされるおそれがあります。
{: tip}

### Watson 製品およびサービス

`gateway.watsonplatform.net` または `stream.wastonplatform.net` を使用して接続している先の Watson 製品やサービスについては、それらを `gateway-tls12.watsonplatform.net` または `stream-tls12.watsonplatform.net` に置き換えてください。 これらの代替エンドポイントは、TLS 1.2 のみをサポートします。 そこに正常に接続できる場合、影響を受けることはありません。 正常に接続できない場合は、影響を受けることになるので、クライアント、クライアント・ライブラリー、またはクライアント構成を変更して、TLS 1.2 に対応できるようにする必要があります。

米国南部以外の地域にある Watson 製品およびサービスの代替エンドポイントは提供されません。それらのエンドポイントでは既に TLS 1.2 しかサポートしていません。

`gatway-tls12.watsonplatform.net` および `stream-tls12.watsonplatform.net` はテスト専用であり、TLS 1.0 および 1.1 が廃止された後は使用できません。
{: tip}

### その他の製品またはサービス

使用可能な代替の TLS 1.2 専用エンドポイントを持たない製品またはサービスの場合、サポートされる TLS のバージョンおよび使用中のバージョンを判別する方法については、提供されているクライアントまたはクライアント・ライブラリーの資料を参照してください。

## TLS 1.0 および 1.1 のサポートを終了する製品およびサービス
{: #prodsandservs}

以下の製品またはサービスで、TLS 1.0 および 1.1 のサポートが終了します。

{{site.data.keyword.Bluemix_notm}} 上の Cloud Foundry や {{site.data.keyword.Bluemix_notm}} カタログ内のサービスなど、一部の製品またはサービスは、複数の地域で提供されていることがあります。 TLS 1.0 および 1.1 は、現在それらがサポートされているすべての地域で廃止されます。

**重要な注:** {{site.data.keyword.Bluemix_notm}} Private または {{site.data.keyword.Bluemix_notm}} Local System デプロイメント、またはそのようなデプロイメントでホストされる {{site.data.keyword.Bluemix_notm}} サービスは含まれません。 ご使用のデプロイメントがまだ TLS 1.0 または 1.1 をサポートしている場合は、顧客またはサポート担当者と相談して廃止する適当な時機を決定してください。

### IBM Cloud カタログから使用可能な製品またはサービス

#### クラウド・プラットフォーム

* {{site.data.keyword.Bluemix_notm}} 上の Cloud Foundry
* {{site.data.keyword.Bluemix_notm}} インフラストラクチャー (`api.softlayer.com` および `api.service.softlayer.com`)

#### API

* API Connect

#### アプリケーション・サービス

* Business Rules
* Message Hub
* Voice Agent with Watson\*
* Watson Content Knowlege Kits\*

#### データ & 分析

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
* Continuous Delivery
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

#### Functions

* Functions

#### インテグレーション

* App Connect
* Product Insights
* Secure Gateway
* API Harmony\*

#### IoT

* 電機向け IoT

#### モバイル

* App ID†
* Mobile Analytics
* Mobile Foundation
* Push Notifications
* App Launch\*

#### セキュリティー

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

\* {{site.data.keyword.Bluemix_notm}} カタログ内の試験サービスとして使用可能です。  
† TLS 1.0 は既に廃止されており、TLS 1.1 のみが廃止されます。  
‡ 非推奨。既存のお客様のみが使用できます。

### IBM Marketplace から使用可能な製品またはサービス

* Forms Experience Builder on Cloud
* IoT for Insurance
* Watson Customer Insight for Insurance
* Watson Marketing Insights
* Watson Knowledge Studio
* Watson Virtual Agent
* Weather Company Energy Trader

### その他の製品またはサービス
{: #prodservices}

* Teacher Advisor with Watson

## 使用している製品またはサービスがリストにない場合、どうしたらいいですか?
{: #tlsprodnotlisted}

ご使用の製品またはサービスは、既に TLS 1.2 しかサポートしていないか、今回は TLS 1.0 および 1.1 を廃止しない可能性があります。 製品またはサービスのエンドポイントで TLS 1.0 および 1.1 がサポートされているかどうかを確認するために使用できる各種クライアント・ツールやオンライン・ツールが提供されています。

## サポート終了後も TLS 1.0 または 1.1 を使用し続けることはできますか?
{: #tlskeepusing}

一部の製品とサービスは、1 次エンドポイントで TLS 1.0 および 1.1 が廃止された後も TLS 1.0 および 1.1 のサポートを継続していく代替エンドポイントを使用可能にしています。

### {{site.data.keyword.Bluemix_notm}} インフラストラクチャー

TLS 1.0 および 1.1 のサポートが `api.softlayer.com` および `api.service.softlayer.com` から外されるときに、TLS 1.0 および 1.1 をサポートする代替エンドポイントが告知され、30 日間使用可能になります。

### Watson 製品およびサービス
{: #watsonprodservices}

サポート終了後も Watson 製品およびサービスに接続するときに引き続き TLS 1.0 または 1.1 を使用する必要がある場合は、`gateway.watsonplatform.net` を `gateway-tls10.wastonplatform.net` に置き換えるか、`stream.watsonplatform.net` を `stream-tls10.watsonplatform.net` に置き換えてください。 `gateway-tls10.watsonplatform.net` と `stream-tls10.watsonplatform.net` は、TLS 1.0、1.1、および 1.2 をサポートし、TLS 1.0 および 1.1 が `gateway.watsonplatform.net` および `stream.watsonplatform.net` で廃止された後も継続して使用できます。

## 連絡
{: #tlssupport}

質問、懸念事項、または問題がある場合、[サポート](https://www.ibm.com/cloud/support)にお問い合わせください。
