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

# Retrait de la prise en charge de TLS 1.0 et 1.1
{: #tlssupportwithdraw}

IBM prévoit de retirer le 1er mars 2018 la prise en charge de TLS 1.0 et 1.1 sur de nombreux produits et services cloud. TLS 1.2 continuera d'être pris en charge pour tous les produits ou services {{site.data.keyword.Bluemix_notm}} retirant la prise en charge pour TLS 1.0 et 1.1.
{:shortdesc}

## Pourquoi ce changement ?
{: #why}

IBM s'est toujours engagé à offrir un cloud totalement sécurisé et conforme aux dernières recommandations de sécurité et de confidentialité.

## Qu'est-ce que TLS ?
{: #what}

Le [protocole TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) est utilisé pour chiffrer les communications effectuées sur un réseau afin de garantir le caractère privé des données. Il existe trois versions différentes de TLS : 1.0, 1.1 et 1.2. Toutes les connexions HTTPS se servent de TLS. HTTPS est la méthode principale utilisée pour s'assurer que vos connexions vers les produits et services {{site.data.keyword.Bluemix_notm}} sont fiables et sécurisées. Certains produits et services {{site.data.keyword.Bluemix_notm}} autorisent les connexions sécurisées qui se servent du protocole WSS (WebSocket Secure) utilisant aussi TLS. Le retrait de la prise en charge pour TLS 1.0 et 1.1 concerne aussi bien les connexions HTTPS que WSS.

## Quelles actions dois-je entreprendre pour m'assurer que je ne serai pas impacté ?
{: #impact}

Une grande partie des connexions effectuées vers les produits ou services {{site.data.keyword.Bluemix_notm}} utilisent déjà TLS 1.2. Si vos connexions ne requièrent pas TLS 1.0 ou 1.1,  vous ne serez pas impacté.

Si vous utilisez l'un des produits ou services qui retirent la prise en charge pour TLS 1.0 ou 1.1, vous devez confirmer que vos connexions n'exigent pas TLS 1.0 ou 1.1.

### Cloud Foundry sur {{site.data.keyword.Bluemix_notm}}

Pour les applications Cloud Foundry, vous devez confirmer que vous ne serez pas impacté quand vous vous connecterez à votre application en dehors de {{site.data.keyword.Bluemix_notm}} ou lors d'une connexion depuis votre application à une autre application Cloud Foundry sur IBM Cloud.

Toutes les connexions à Cloud Foundry qui utilisent TLS sont potentiellement impactées, incluant les connexions effectuées depuis des navigateurs Web. Tous les navigateurs les plus récents prennent en charge TLS 1.2, incluant les navigateurs prérequis pour [{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/overview/prereqs.html#browsers).
{: tip}

#### Connexion à votre application Cloud Foundry

Tous les noeuds finaux d'application Cloud Foundry sur le domaine `*.mybluemix.net` peuvent être accédés via un noeud final alternatif qui ne prend en charge que TLS 1.2.

Pour utiliser le noeud final alternatif, ajoutez `alt.` après le sous-domaine de votre application : ainsi, si votre application est hébergée sur `https://myapplication.mybluemix.net`, utilisez `https://myapplication.alt.mybluemix.net`, ou pour `https://myaplication.eu-gb.mybluemix.net`, utilisez `https://myapplication.alt.eu-gb.mybluemix.net`.

Si vous parvenez à vous connecter au noeud final alternatif, vous ne serez pas impacté.

Un échec de connexion indique que vous serez touché et qu'il vous faut donc modifier votre client, les bibliothèques client ou la configuration client pour activer TLS 1.2.

#### Connexion entre applications Cloud Foundry

Vous pouvez configurer votre application Cloud Foundry pour une redirection automatique vers les noeuds finaux alternatifs disponibles sur le domaine `*.mybluemix.net` lors de la connexion à d'autres applications, en utilisant la commande suivante :
```
cf <nom_application> BLUEMIX_TLS10_DISABLED true
```

Une fois que vous avez défini `BLUEMIX_TLS10_DISABLED` à `true`, votre application doit être reconstituée en utilisant la commande suivante, pour que ce changement prenne effet :
```
cf restage <nom_application>
```

Une fois que vous avez effectué ces changements, toute demande sortante en provenance de votre application est redirigée vers les noeuds finaux alternatifs TLS 1.2 uniquement.

Pour utiliser les noeuds finaux alternatifs, votre client doit prendre en charge l'extension TLS SNI (Server Name Indication). Si ce n'est pas le cas, le certificat retourné risque d'être considéré comme non valide par votre client et vous risquez de supposer à tort que vous êtes impacté par le retrait de TLS 1.0 et 1.1.
{: tip}

### Produits et services Watson

Pour les produits et services Watson auxquels vous vous connectez en utilisant `gateway.watsonplatform.net` ou `stream.wastonplatform.net`, remplacez ces derniers par `gateway-tls12.watsonplatform.net` ou `stream-tls12.watsonplatform.net`. Ces noeuds finaux alternatifs ne prennent en charge que TLS 1.2. Si vous parvenez à vous y connecter, vous ne serez pas impacté. Un échec de connexion indique que vous serez touché et qu'il vous faut donc modifier votre client, les bibliothèques client ou la configuration client pour activer TLS 1.2.

Aucun noeud final alternatif pour les produits et services Watson dans des régions autres que Sud des Etats-Unis n'est fourni car elles prennent déjà en charge TLS 1.2.

`gatway-tls12.watsonplatform.net` et `stream-tls12.watsonplatform.net` sont fournis à des fins de test uniquement et ne seront plus disponibles après le retrait de TLS 1.0 et 1.1.
{: tip}

### Autres produits ou services

Pour les produits ou services qui ne disposent pas de noeuds finaux alternatifs TLS 1.2 uniquement, reportez-vous à la documentation disponible pour votre client ou vos bibliothèques client pour plus d'informations sur la façon de déterminer les versions de TLS qui sont prises en charge et la version que vous utilisez.

## Quels sont les produits et services qui retirent leur prise en charge pour TLS 1.0 et 1.1 ?
{: #prodsandservs}

Les produits et services ci-après retirent leur prise en charge pour TLS 1.0 et 1.1.

Certains produits ou services, comme Cloud Foundry on {{site.data.keyword.Bluemix_notm}} et les services du catalogue {{site.data.keyword.Bluemix_notm}} peuvent être proposés dans plusieurs régions différentes. TLS 1.0 et 1.1 seront retirés dans toutes les régions dans lesquelles ils sont actuellement pris en charge.

**Remarque importante :** les déploiements de système {{site.data.keyword.Bluemix_notm}} privé ou {{site.data.keyword.Bluemix_notm}} local ou tous les services {{site.data.keyword.Bluemix_notm}} hébergés dans ces déploiements ne sont pas inclus. Si votre déploiement prend toujours en charge TLS 1.0 ou 1.1, voyez avec votre responsable client ou support quand effectuer le retrait .

### Produits ou services disponibles depuis le catalogue IBM Cloud

#### Plateforme cloud

* Cloud Foundry sur {{site.data.keyword.Bluemix_notm}}
* Infrastructure {{site.data.keyword.Bluemix_notm}} (`api.softlayer.com` et `api.service.softlayer.com`)

#### API

* API Connect

#### Services d'application

* Business Rules
* Message Hub
* Voice Agent with Watson\*
* Watson Content Knowledge Kits\*

#### Données et analyse

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

#### Finance

* Historical Instrument Analytics\*
* Instrument Analytics\*
* Investment Portfolio\*
* Portfolio Optimization\*
* Predictive Market Scenarios\*
* Simulated Historical Instrument Analytics\*
* Simulated Instrument Analytics\*

#### Fonctions

* Fonctions

#### Intégration

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

#### Sécurité

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

\* Disponible dans la catégorie services expérimentaux du catalogue {{site.data.keyword.Bluemix_notm}}.  
† TLS 1.0 a déjà été retiré, seul TLS 1.1 est concerné par le retrait actuel.  
‡ Déprécié, disponible uniquement pour les clients existants.

### Produits ou services disponibles depuis IBM Marketplace

* Forms Experience Builder on Cloud
* IoT for Insurance
* Watson Customer Insight for Insurance
* Watson Marketing Insights
* Watson Knowledge Studio
* Watson Virtual Agent
* Weather Company Energy Trader

### Autres produits ou services
{: #prodservices}

* Teacher Advisor with Watson

## Que faire si mon produit ou service n'est pas répertorié ?
{: #tlsprodnotlisted}

Il est possible que votre produit ou service prenne déjà en charge TLS 1.2 ou ne procède pas au retrait de TLS 1.0 et 1.1 pour le moment. Différents outils client et en ligne sont disponibles que vous pouvez utiliser pour vérifier si TLS 1.0 et 1.1 sont pris en charge par un produit ou des noeuds finaux de service.

## Il y a-t-il une façon de continuer à utiliser TLS 1.0 ou 1.1 une fois la prise en charge retirée ?
{: #tlskeepusing}

Certains produits et services mettent à disposition des noeuds finaux alternatifs qui continuent à prendre en charge TLS 1.0 et 1.1 une fois que ces derniers sont retirés des noeuds finaux principaux.

### Infrastructure {{site.data.keyword.Bluemix_notm}}

Quand la prise en charge pour TLS 1.0 et 1.1 sera retirée de `api.softlayer.com` et `api.service.softlayer.com`, des noeuds finaux alternatifs prenant en charge TLS 1.0 et 1.1 seront annoncés et mis à disposition pendant 30 jours.

### Produits et services Watson
{: #watsonprodservices}

Si vous devez continuer à utiliser TLS 1.0 ou 1.1 lors d'une connexion aux produits et services Watson une fois le support retiré, vous pouvez remplacer `gateway.watsonplatform.net` par `gateway-tls10.wastonplatform.net` ou `stream.watsonplatform.net` par `stream-tls10.watsonplatform.net`. `gateway-tls10.watsonplatform.net` et `stream-tls10.watsonplatform.net`, qui prennent en charge TLS 1.0, 1.1 et 1.2, continueront à être disponibles pour utilisation une fois TLS 1.0 et 1.1 retirés de `gateway.watsonplatform.net` et `stream.watsonplatform.net`.

## Contactez-nous
{: #tlssupport}

Si vous avez des questions, des doutes ou des problèmes, contactez le [support](https://www.ibm.com/cloud/support).
