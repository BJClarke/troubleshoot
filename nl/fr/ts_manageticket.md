---

copyright:

  years: 2015, 2018

lastupdated: "2017-11-09"

---


{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}


# Traitement des incidents liés à la gestion des tickets de demande de service
{: #SupportTickets}

Les incidents des tickets {{site.data.keyword.Bluemix}} peuvent inclure une incapacité à gérer les tickets de demande de service {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Les comptes liés ne peuvent pas ajouter ni éditer de tickets de demande de service
{: #ts_service_broker}

Si vous disposez d'un compte lié, il est possible que vous ne puissiez pas ajouter ou éditer des tickets de demande de service {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Impossible de créer ou d'éditer des tickets de demande de service dans {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

Lorsque vous disposez d'un compte lié, les problèmes les plus courants liés à la gestion des tickets de demande de service peuvent être provoqués par une absence de paramétrage de compte avec plus de granularité fine dans le portail {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.slportal}}. Etant donné que vous devez configurer des droits avec plus de granularité fine sur les comptes créés dans le portail {{site.data.keyword.slportal}}, il est possible que vous ne puissiez pas ajouter ou éditer des tickets de demande de service.
{: tsCauses}

Pour résoudre ce problème, contactez l'administrateur de compte {{site.data.keyword.slportal}} afin qu'il définisse les accès appropriés sur votre compte. L'administrateur de compte {{site.data.keyword.slportal}} peut résoudre le problème comme suit :

1. Dans le menu du portail {{site.data.keyword.slportal}} **Compte**, sélectionnez **Utilisateurs**.
2. Sélectionner l'utilisateur dans la liste.
3. Sur le profil utilisateur, dans **Portal Permissions**, sélectionnez l'onglet **Support**, puis cliquez pour fournir à l'utilisateur les droits appropriés d'affichage, d'ajout et d'édition des tickets de demande de service.
{: tsResolve}
