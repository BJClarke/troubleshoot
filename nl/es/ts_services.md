---

copyright:

  years: 2015, 2018

lastupdated: "2017-11-07"

---


{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}


# Resolución de problemas de servicios
{: #services}

Entre los problemas de los servicios de {{site.data.keyword.Bluemix}}
se pueden incluir los errores de tiempo de espera agotado de pasarela que se producen al suprimir
una instancia de servicio. Puede solucionar estos problemas siguiendo unos sencillos pasos.
{:shortdesc}

## El error de intermediario de servicio se produce al suprimir una instancia de servicio
{: #ts_service_broker}

Es posible que reciba un mensaje de error cuando intente suprimir una instancia de servicio que ya se ha suprimido desde el controlador de la nube.
{:shortdesc}

Cuando intenta suprimir una instancia de servicio, ve el siguiente mensaje de error del intermediario de servicios:
{: tsSymptoms}
`Tiempo de espera excedido de pasarela`

Este problema sucede si la instancia de servicio ya se ha suprimido desde el controlador de la nube.
{: tsCauses}

Cree una instancia de servicio con el mismo nombre de servicio y luego enlácela a las aplicaciones. A continuación, puede suprimir la instancia de servicio y las apps que utilizan el servicio.   
{: tsResolve}
