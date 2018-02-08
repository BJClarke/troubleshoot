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


# Traitement des incidents liés aux services
{: #services}

Des problèmes liés au service {{site.data.keyword.Bluemix}} peuvent survenir, par exemple, une erreur de dépassement de délai d'attente de la passerelle peut se produire lorsque vous supprimez une instance de service. Ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}

## Une erreur du courtier de services se produit lorsque vous supprimez une instance de service
{: #ts_service_broker}

Il se peut que vous receviez un message d'erreur lorsque vous tentez de supprimer une instance de service qui a déjà été supprimée du contrôleur de cloud.
{:shortdesc}

Lorsque vous tentez de supprimer une instance de service, le message d'erreur de courtier de services suivant s'affiche :
{: tsSymptoms}
`Gateway timeout`

Ce problème se produit lorsque l'instance de service a déjà été supprimée du contrôleur de cloud.
{: tsCauses}

Créez une instance de service portant le même nom de service et liez-la à vos applications. Vous pouvez ensuite supprimer l'instance de service et les applications qui utilisent ce service.   
{: tsResolve}
