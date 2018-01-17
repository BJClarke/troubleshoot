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

# Retirada de suporte para o TLS 1.0 e 1.1
{: #tlssupportwithdraw}

A IBM irá retirar o suporte para o TLS 1.0 e TLS 1.1 em muitos dos nossos produtos e serviços de nuvem em 1º de março de 2018. O TLS 1.2 continuará a ser suportado para qualquer produto ou serviço do {{site.data.keyword.Bluemix_notm}} que estiver retirando o suporte para o TLS 1.0 e 1.1.
{:shortdesc}

## Por que estamos fazendo essa mudança?
{: #why}

Isso faz parte do compromisso da IBM em oferecer uma nuvem que seja segura para o núcleo e em alinhamento com as melhores práticas do segmento de mercado para segurança e privacidade de dados.

## O que é TLS?
{: #what}

O [protocolo TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) é usado para criptografar as comunicações em uma rede para assegurar que os dados transmitidos permaneçam privados. Há três versões liberadas do TLS: 1.0, 1.1 e 1.2. Todas as conexões HTTPS usam o TLS. HTTPS é o método predominante de assegurar que suas conexões com produtos e serviços do {{site.data.keyword.Bluemix_notm}} sejam confiáveis e seguras. Alguns produtos e serviços do {{site.data.keyword.Bluemix_notm}} permitem conexões seguras usando o protocolo WebSocket Secure (WSS) que também usa TLS. A retirada de suporte para o TLS 1.0 e o 1.1 abrange as conexões HTTPS e WSS.

## Quais ações eu preciso tomar para garantir que não serei afetado?
{: #impact}

Uma maioria significativa de conexões feitas para produtos ou serviços do {{site.data.keyword.Bluemix_notm}} já usa o TLS 1.2. Se suas conexões não requererem o TLS 1.0 ou 1.1, você não será afetado. 

Se você está usando qualquer um dos produtos de serviços que estão retirando o suporte para TLS 1.0 ou 1.1, deve-se confirmar que suas conexões não requerem TLS 1.0 ou 1.1.

### Cloud Foundry no {{site.data.keyword.Bluemix_notm}}

Para aplicativos Cloud Foundry, você precisará confirmar que não será afetado quando se conectar ao seu aplicativo de fora do {{site.data.keyword.Bluemix_notm}} ou quando se conectar de seu aplicativo a outro aplicativo Cloud Foundry no IBM Cloud.

Todas as conexões com o Cloud Foundry que usam o TLS são potencialmente afetadas, incluindo quaisquer conexões feitas de navegadores da web. Todos os navegadores modernos suportam o TLS 1.2, incluindo aqueles que são pré-requisitos para o [{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/overview/prereqs.html#browsers).
{: tip}

#### Conectando-se ao seu aplicativo Cloud Foundry

Todos os terminais de aplicativo Cloud Foundry no domínio `*.mybluemix.net` podem ser acessados por meio de um terminal alternativo que suporta somente o TLS 1.2. 

Para usar o terminal alternativo, inclua `alt.` após o subdomínio do seu aplicativo, por exemplo, se seu aplicativo está hospedado em `https://myapplication.mybluemix.net`, use `https://myapplication.alt.mybluemix.net`. Ou, para `https://myaplication.eu-gb.mybluemix.net`, use `https://myapplication.alt.eu-gb.mybluemix.net`.

Se estiver apto a conectar-se com êxito ao terminal alternativo, você não será afetado. 

Se não for possível se conectar com êxito, você será afetado. Então, deve-se mudar seu cliente, as bibliotecas do cliente ou a configuração do cliente para ativar o TLS 1.2.

#### Conectando entre aplicativos Cloud Foundry

Será possível configurar seu aplicativo Cloud Foundry para redirecionar automaticamente para os terminais alternativos disponíveis no domínio `*.mybluemix.net` quando se conectar a outros aplicativos usando o comando a seguir:
```
cf <application_name> BLUEMIX_TLS10_DISABLED true
```

Depois de configurar `BLUEMIX_TLS10_DISABLED` para `true`, seu aplicativo deve ser remontado usando o comando a seguir para que essa mudança entre em vigor:
```
cf restage <application_name>
```

Após fazer essas mudanças, qualquer solicitação de saída do seu aplicativo será redirecionada para os terminais alternativos somente TLS 1.2.

Para usar os terminais alternativos, o cliente deve suportar a extensão do TLS Server Name Indication (SNI). Se não, o certificado retornado pode ser considerado inválido por seu cliente. Se isso ocorre, você pode supor incorretamente que foi afetado pela remoção do TLS 1.0 e 1.1.
{: tip}

### Produtos e serviços Watson

Para produtos e serviços do Watson aos quais você se conecta usando `gateway.watsonplatform.net` ou `stream.wastonplatform.net`, substitua-os por `gateway-tls12.watsonplatform.net` ou `stream-tls12.watsonplatform.net`. Esses terminais alternativos suportam somente o TLS 1.2. Se estiver apto a conectar-se com êxito a eles, você não será afetado. Se não for possível se conectar com êxito, você será afetado. Então, deve-se mudar seu cliente, as bibliotecas do cliente ou a configuração do cliente para ativar o TLS 1.2.

Os terminais alternativos para produtos e serviços do Watson em regiões diferentes do Sul dos Estados Unidos não são fornecidos, pois eles já suportam somente o TLS 1.2.

`gatway-tls12.watsonplatform.net` e `stream-tls12.watsonplatform.net` são somente para propósitos de teste e não estarão disponíveis após o TLS 1.0 e o 1.1 serem removidos.
{: tip}

### Outros produtos ou serviços

Para produtos ou serviços que não têm os terminais alternativos somente do TLS 1.2 disponíveis, consulte qualquer documentação disponível para seu cliente ou bibliotecas do cliente para obter informações sobre como determinar quais versões do TLS são suportadas e qual versão você está usando.

## Quais produtos e serviços estão retirando o suporte para o TLS 1.0 e 1.1?
{: #prodsandservs}

Os produtos ou serviços a seguir estão retirando o suporte para o TLS 1.0 e 1.1.

Alguns produtos ou serviços, como o Cloud Foundry no {{site.data.keyword.Bluemix_notm}} e os serviços no catálogo do {{site.data.keyword.Bluemix_notm}}, podem ser oferecidos em múltiplas regiões. O TLS 1.0 e o 1.1 serão removidos de todas as regiões em que eles são suportados atualmente.

**Nota importante:** as implementações do {{site.data.keyword.Bluemix_notm}} Private ou {{site.data.keyword.Bluemix_notm}} Local System ou quaisquer serviços do {{site.data.keyword.Bluemix_notm}} hospedados nessas implementações não são incluídos. Se a sua implementação ainda suporta o TLS 1.0 ou 1.1, trabalhe com seu cliente ou representante de suporte para determinar quando a remoção é correta para você.

### Produtos ou serviços disponíveis no catálogo do IBM Cloud

#### Plataforma de nuvem

* Cloud Foundry no {{site.data.keyword.Bluemix_notm}}
* Infraestrutura do {{site.data.keyword.Bluemix_notm}} (`api.softlayer.com` e `api.service.softlayer.com`)

#### APIs

* API Connect

#### Serviços de Aplicativos

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
* Conexão de dados
* Data Refinary
* Otimização de Decisão
* Gráfico
* Informix
* Lift
* Dados da empresa de clima
* Managed MS-SQL Database Server\*

#### DevOps

* Auto-Scaling
* Alert Notification
* Availability Monitoring
* Continuous Release
* DevOps Insights
* Gerenciamento de eventos
* Globalization Pipeline
* Automated Accessibility Tester\*
* Digital Content Checker\*
* Runbook Automation\*

#### Finança

* Historical Instrument Analytics\*
* Instrument Analytics\*
* Investment Portfolio\*
* Portfolio Optimization\*
* Predictive Market Scenarios\*
* Simulated Historical Instrument Analytics\*
* Simulated Instrument Analytics\*

#### Funções

* Funções

#### Integrar

* App Connect
* Product Insights
* Secure Gateway
* API Harmony\*

#### Internet of Things

* IoT para Eletroeletrônico

#### Mobile

* ID do app†
* Mobile Analytics
* Mobile Foundation
* Push Notifications
* App Launch\*

#### Segurança

* ID do app†
* Certificados SSL† 

#### Watson

* Conversa
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

\* Disponível sob serviços experimentais no catálogo do {{site.data.keyword.Bluemix_notm}}.  
† O TLS 1.0 já foi removido, somente o TLS 1.1 está sendo removido.  
‡ Descontinuado, disponível somente para clientes existentes. 

### Produtos ou serviços disponíveis por meio do mercado de profissionais IBM

* Forms Experience Builder on Cloud
* IoT for Insurance
* Watson Customer Insight for Insurance
* Watson Marketing Insights
* Watson Knowledge Studio
* Watson Virtual Agent
* Weather Company Energy Trader

### Outros produtos ou serviços

* Teacher Advisor with Watson

## E se meu produto ou serviço não está listado?
{: #tlsprodnotlisted}

Seu produto ou serviço pode já suportar somente o TLS 1.2 ou talvez não esteja removendo o TLS 1.0 e 1.1 neste momento. Há várias ferramentas on-line e de cliente disponíveis que podem ser usadas para verificar se o TLS 1.0 e o 1.1 são suportados ou não pelos terminais de um produto ou serviço.

Produtos ou serviços adicionais podem ser incluídos nesse comunicado em 05 de janeiro de 2018 ou antes.

## Existe uma maneira de poder continuar usando o TLS 1.0 ou 1.1 após o suporte ser retirado?
{: #tlskeepusing}

Alguns produtos e serviços estão tornando disponíveis terminais alternativos que continuarão a suportar o TLS 1.0 e o 1.1 após o TLS 1.0 e o 1.1 serem removidos dos terminais primários.

### Infraestrutura do {{site.data.keyword.Bluemix_notm}}

Quando o suporte para o TLS 1.0 e 1.1 for removido de `api.softlayer.com` e `api.service.softlayer.com`, os terminais alternativos que suportam o TLS 1.0 e 1.1 serão anunciados e disponibilizados por 30 dias. 

### Produtos e serviços Watson

Se você precisar continuar a usar o TLS 1.0 ou 1.1 quando se conectar a produtos e serviços do Watson após o suporte ser retirado, será possível substituir `gateway.watsonplatform.net` por `gateway-tls10.wastonplatform.net` ou `stream.watsonplatform.net` por `stream-tls10.watsonplatform.net`. O `gateway-tls10.watsonplatform.net` e o `stream-tls10.watsonplatform.net` suportam o TLS 1.0, 1.1 e 1.2 e continuarão disponíveis para uso após o TLS 1.0 e o 1.1 serem removidos de `gateway.watsonplatform.net` e `stream.watsonplatform.net`.

## Entre em contato
{: #tlssupport}

Se você tiver quaisquer perguntas, preocupações ou problemas, entre em contato com o [Suporte](https://www.ibm.com/cloud/support).
