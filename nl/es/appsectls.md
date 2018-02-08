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

# Retirada de soporte para TLS 1.0 y 1.1
{: #tlssupportwithdraw}

IBM retirará el soporte para TLS 1.0 y TLS 1.1 en muchos productos y servicios de nube el 1 de marzo de 2018. TLS 1.2 seguirá teniendo soporte para cualquier producto o servicio de {{site.data.keyword.Bluemix_notm}} en el que se retire el soporte para TLS 1.0 y 1.1.
{:shortdesc}

## ¿Por qué hacemos este cambio?
{: #why}

Esto es parte del compromiso de IBM para ofrecer una nube que sea completamente segura y acorde con las mejores prácticas de la industria para la seguridad y la privacidad de los datos.

## ¿Qué es TLS?
{: #what}

El [protocolo TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) se utiliza para cifrar las comunicaciones en una red para garantizar que los datos transmitidos sean privados. Existen tres versiones publicadas de TLS: 1.0, 1.1 y 1.2. Todas las conexiones HTTPS utilizan TLS. HTTPS es el método predominante para garantizar que las conexiones a los productos y servicios de {{site.data.keyword.Bluemix_notm}} son fiables y seguras. Algunos productos y servicios de {{site.data.keyword.Bluemix_notm}} permiten conexiones seguras mediante el protocolo WebSocket Secure (WSS), que también utiliza TLS. La retirada de soporte para TLS 1.0 y 1.1 abarca las conexiones HTTPS y WSS.

## ¿Qué medidas debo tomar para no verme afectado?
{: #impact}

La gran mayoría de las conexiones realizadas a productos y servicios de {{site.data.keyword.Bluemix_notm}} ya utiliza TLS 1.2. Si sus conexiones no requieren TLS 1.0 o 1.1, no se verá afectado.

Si utiliza cualquiera de los productos o servicios en los que se va a retirar el soporte para TLS 1.0 o 1.1, debe confirmar que sus conexiones no requieren TLS 1.0 o 1.1.

### Cloud Foundry en {{site.data.keyword.Bluemix_notm}}

Para las aplicaciones de Cloud Foundry, debe confirmar que no se verá afectado cuando se conecte a la aplicación desde fuera de {{site.data.keyword.Bluemix_notm}} o cuando se conecte desde la aplicación a otra aplicación de Cloud Foundry en IBM Cloud.

Todas las conexiones a Cloud Foundry que utilicen TLS se pueden ver afectadas, incluidas las conexiones realizadas desde los navegadores web. Todos los navegadores modernos son compatibles con TLS 1.2, incluidos los que son requisitos previos para [{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/overview/prereqs.html#browsers).
{: tip}

#### Conexión a la aplicación de Cloud Foundry

Se puede acceder a todos los puntos finales de aplicación de Cloud Foundry del dominio `*.mybluemix.net` mediante un punto final alternativo que solo admite TLS 1.2.

Para utilizar el punto final alternativo, añada `alt.` después del subdominio de la aplicación, por ejemplo, si la aplicación está alojada en `https://myapplication.mybluemix.net`, utilice `https://myapplication.alt.mybluemix.net`. O, para `https://myaplication.eu-gb.mybluemix.net`, utilice `https://myapplication.alt.eu-gb.mybluemix.net`.

Si se puede conectar correctamente con el punto final alternativo, no se verá afectado.

Si no se puede conectar correctamente, se verá afectado y debe cambiar el cliente, las bibliotecas de cliente o la configuración de cliente para habilitar TLS 1.2.

#### Conexión entre aplicaciones de Cloud Foundry

Puede configurar la aplicación de Cloud Foundry para redirigir automáticamente a los puntos finales alternativos disponibles en el dominio `*.mybluemix.net` al conectarse a otras aplicaciones utilizando el mandato siguiente:
```
cf <application_name> BLUEMIX_TLS10_DISABLED true
```

Después de establecer `BLUEMIX_TLS10_DISABLED` en `true`, debe volver a transferir la aplicación utilizando el mandato siguiente para que se aplique este cambio:
```
cf restage <application_name>
```

Tras realizar estos cambios, las solicitudes salientes de su aplicación se redirigirán solo a los puntos finales alternativos de TLS 1.2.

Para utilizar los puntos finales alternativos, el cliente debe ser compatible con la extensión de TLS Server Name Indication (SNI). Si no lo es, puede que el cliente considere no válido el certificado devuelto. Si esto sucede, puede que presuponga incorrectamente que le afecta la retirada de TLS 1.0 y 1.1.
{: tip}

### Productos y servicios de Watson

Para los productos y los servicios de Watson a los que se conecta mediante `gateway.watsonplatform.net` o `stream.wastonplatform.net`, sustituya esos valores con `gateway-tls12.watsonplatform.net` o `stream-tls12.watsonplatform.net`. Estos puntos finales alternativos solo admiten TLS 1.2. Si se puede conectar correctamente con ellos, no se verá afectado. Si no se puede conectar correctamente, se verá afectado y debe cambiar el cliente, las bibliotecas de cliente o la configuración de cliente para habilitar TLS 1.2.

No se proporcionan puntos finales alternativos para productos y servicios de Watson en otras regiones diferentes a EE.UU. sur, ya que estas ya admiten solo TLS 1.2.

`gatway-tls12.watsonplatform.net` y `stream-tls12.watsonplatform.net` son solo para pruebas y no estarán disponibles tras la retirada de TLS 1.0 y 1.1.
{: tip}

### Otros productos o servicios

Para productos o servicios que no tienen puntos finales alternativos de solo TLS 1.2 disponibles, consulte cualquier documentación disponible para el cliente o las bibliotecas de cliente para obtener información sobre cómo determinar qué versiones de TLS están soportadas y qué versión está utilizando.

## ¿Qué productos y servicios van a retirar el soporte para TLS 1.0 y 1.1?
{: #prodsandservs}

Los siguientes productos o servicios van a retirar el soporte para TLS 1.0 y 1.1.

Algunos productos o servicios, como por ejemplo Cloud Foundry en {{site.data.keyword.Bluemix_notm}} y servicios del catálogo de {{site.data.keyword.Bluemix_notm}}, pueden ofrecerse en varias regiones. TLS 1.0 y 1.1 se eliminarán en todas las regiones donde están soportados actualmente.

**Nota importante:** no se incluyen los despliegues de {{site.data.keyword.Bluemix_notm}} Private o {{site.data.keyword.Bluemix_notm}} Local System, ni ningún servicio de {{site.data.keyword.Bluemix_notm}} alojado en estos despliegues. Si su despliegue todavía admite TLS 1.0 o 1.1, valore con su representante de soporte o cliente el momento adecuado de la retirada.

### Productos o servicios disponibles en el catálogo de IBM Cloud

#### Plataforma cloud

* Cloud Foundry en {{site.data.keyword.Bluemix_notm}}
* Infraestructura de {{site.data.keyword.Bluemix_notm}} (`api.softlayer.com` y `api.service.softlayer.com`)

#### API

* API Connect

#### Servicios de aplicación

* Business Rules
* Message Hub
* Voice Agent with Watson\*
* Watson Content Knowlege Kits\*

#### Datos y análisis

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

#### Finanzas

* Historical Instrument Analytics\*
* Instrument Analytics\*
* Investment Portfolio\*
* Portfolio Optimization\*
* Predictive Market Scenarios\*
* Simulated Historical Instrument Analytics\*
* Simulated Instrument Analytics\*

#### Funciones

* Funciones

#### Integrar

* App Connect
* Product Insights
* Secure Gateway
* API Harmony\*

#### Internet de las cosas

* IoT for Electronics

#### Móvil

* App ID†
* Mobile Analytics
* Mobile Foundation
* Push Notifications
* App Launch\*

#### Seguridad

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

\*Disponible en servicios experimentales en el catálogo de {{site.data.keyword.Bluemix_notm}}.  
† TLS 1.0 ya se ha eliminado, solo se va a eliminar TLS 1.1.  
‡ En desuso, solo disponible para clientes actuales.

### Productos o servicios disponibles a través de IBM Marketplace

* Forms Experience Builder on Cloud
* IoT for Insurance
* Watson Customer Insight for Insurance
* Watson Marketing Insights
* Watson Knowledge Studio
* Watson Virtual Agent
* Weather Company Energy Trader

### Otros productos o servicios
{: #prodservices}

* Teacher Advisor with Watson

## ¿Qué pasa si mi producto o servicio no está en la lista?
{: #tlsprodnotlisted}

Puede que su producto o servicio ya admita sólo TLS 1.2 o no vaya a eliminar TLS 1.0 y 1.1 en este momento. Hay varias herramientas de cliente y en línea disponibles que puede utilizar para comprobar si TLS 1.0 y 1.1 están soportados por los puntos finales de un producto o servicio.

## ¿Hay alguna forma de poder seguir utilizando TLS 1.0 o 1.1 una vez retirado el soporte?
{: #tlskeepusing}

Algunos productos y servicios están proporcionando puntos finales alternativos que seguirán admitiendo TLS 1.0 y 1.1 después de que TLS 1.0 y 1.1 se retiren de los puntos finales principales.

### Infraestructura de {{site.data.keyword.Bluemix_notm}}

Cuando se elimine el soporte para TLS 1.0 y 1.1 de `api.softlayer.com` y `api.service.softlayer.com`, se anunciarán puntos finales alternativos que admitan TLS 1.0 y 1.1 y estarán disponibles durante 30 días.

### Productos y servicios de Watson
{: #watsonprodservices}

Si necesita seguir utilizando TLS 1.0 o 1.1 para conectarse a productos y servicios de Watson una vez que se haya retirado el soporte, puede sustituir `gateway.watsonplatform.net` por `gateway-tls10.wastonplatform.net` o `stream.watsonplatform.net` por `stream-tls10.watsonplatform.net`. `gateway-tls10.watsonplatform.net` y `stream-tls10.watsonplatform.net` admiten TLS 1.0, 1.1 y 1.2 y seguirán estando disponibles una vez que TLS 1.0 y 1.1 se hayan eliminado de `gateway.watsonplatform.net` y `stream.watsonplatform.net`.

## Póngase en contacto
{: #tlssupport}

Si tiene alguna pregunta, duda o problema, póngase en contacto con el equipo de [soporte](https://www.ibm.com/cloud/support).
