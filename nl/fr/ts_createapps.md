---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-16"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Traitement des incidents liés à la création d'applications
{: #troubleshoot}

Les problèmes d'ordre général liés à l'utilisation du plug-in {{site.data.keyword.dev_cli_short}} pour créer des applications peuvent inclure des échecs de déploiement ou l'échec de l'extraction du code lors de la création d'un projet. Dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}

## Erreur de nom d'hôte lors de la création d'un projet avec un pattern non mobile
{: #hostname-error}

L'erreur suivante peut s'afficher si vous utilisez le plug-in {{site.data.keyword.dev_cli_short}} pour créer un projet depuis les modèles Application Web, BFF ou Microservice :

```
The hostname <myHostname> is taken.
```
{: codeblock}
{: tsSymptoms}
   
Cette erreur est provoquée par un jeton de connexion ayant expiré.
{: tsCauses}

Connectez-vous à nouveau.

```
bx login
```
{: codeblock}
{: tsResolve}

## Défaillances générales au niveau du plug-in {{site.data.keyword.dev_cli_short}}
{: #general}

L'erreur suivante peut s'afficher si vous utilisez les commandes {{site.data.keyword.dev_cli_short}} `create`, `delete`, `list` ou `code` :

```
Failed to <command> project.
```
{: codeblock}
{: tsSymptoms}
   
Cette erreur est provoquée par un jeton de connexion ayant expiré.
{: tsCauses}

Connectez-vous à nouveau.

```
bx login
```
{: codeblock}
{: tsResolve}

## Erreur : aucune image de ce type lorsque vous exécutez un nouveau projet
{: #nosuchimage}

L'erreur suivante peut s'afficher lorsque vous exécutez un projet alors que vous ne l'avez pas généré :

```
$ bx dev run testProject
L'option run-cmd n'a pas été spécifiée
Arrêt du conteneur 'testProject' en cours...
Le conteneur 'testProject' est introuvable
Création de l'image bx-dev-testProject basée sur Dockerfile en cours...
OK
Création d'un conteneur nommé 'testProject' à partir de cette image en cours...
ECHEC
Le conteneur 'testProject' n'a pas pu être créé :
Erreur : Pas d'image de ce type : bx-dev-testProject
```
{: tsSymptoms}

Vous devez générer un projet avant de l'exécuter. 
{: tsCauses}

Exécutez la commande suivante dans votre répertoire de projet en cours pour générer votre application :

```
bx dev build
```
{: codeblock}

Exécutez la commande suivante dans votre répertoire de projet en cours pour démarrer votre application :

```
bx dev run
```
{: tsResolve}

## Erreur du courtier de services lorsque vous ajoutez la fonction {{site.data.keyword.objectstorageshort}}
{: #os}

L'erreur suivante peut s'afficher si vous utilisez le plug-in {{site.data.keyword.dev_cli_short}} pour créer deux projets avec la fonctionnalité {{site.data.keyword.objectstorageshort}} :

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}
{: tsSymptoms}
   
Cette erreur est liée au service {{site.data.keyword.objectstorageshort}}, qui ne fournit qu'une seule instance du plan {{site.data.keyword.objectstorageshort}} gratuit.
{: tsCauses}

Choisissez un autre plan pour éviter cette erreur.
{: tsResolve}

## Echec de l'obtention du code lors de la création d'un projet
{: #code}

L'erreur suivante peut s'afficher si vous utilisez le plug-in {{site.data.keyword.dev_cli_short}} pour créer un projet :
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
{: tsSymptoms}

Cette erreur est due à un dépassement de délai interne.
{: tsCauses}

Vous pouvez obtenir le code de l'une des façons suivantes :

* Exécutez la commande suivante en utilisant l'interface de ligne de commande :

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   Remplacez `<your-project-name>` par le nom de projet que vous avez spécifié au cours de la création du projet.

* Utilisez la console {{site.data.keyword.dev_console}}.

	1. Sélectionnez votre [projet ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://console.{DomainName}/developer/projects) dans la console {{site.data.keyword.dev_console}} et cliquez sur **Obtenir le code**.

	2. Cliquez sur **Générer le code**.

	3. Une fois le code généré, cliquez sur **Télécharger le code**.
{: tsResolve}

## Erreur lors de l'exécution de `bx dev run` pour les projets Node.js
{: #node}

L'erreur suivante peut s'afficher si vous exécutez `bx dev run` avec des projets Web or BFF du plug-in {{site.data.keyword.dev_cli_short}} for Node.js :

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}
{: tsSymptoms}
   
Cette erreur survient lorsque le module `appmetrics` est installé dans une architecture différente. Les modules npm natifs qui sont installés sur une architecture ne fonctionnent pas sur une autre architecture. Les images Docker incluses sont basées sur le noyau Linux.
{: tsCauses}

Supprimez le dossier `node_modules` et relancez l'exécution de la commande `bx dev run`.
{: tsResolve}

## Echec du déploiement sur {{site.data.keyword.Bluemix_notm}}

Une erreur se produit lorsque vous tentez d'effectuer un déploiement sur {{site.data.keyword.Bluemix_notm}} avec le plug-in {{site.data.keyword.dev_cli_short}} et qu'aucune erreur ne s'affiche.
{: tsSymptoms}

Vous n'êtes peut-être pas connecté à votre compte.
{: tsCauses}

Connectez-vous et réessayez.

```
bx login
```
{: tsResolve}

## Echec du déploiement sur Kubernetes sur {{site.data.keyword.Bluemix_notm}}

L'erreur suivante peut s'afficher après que vous avez entré votre nom de cluster : 

```
FAILED
Failed to execute the action:  exit status 1:

FAILED
Failed to configure deployment with cluster '<cluster-name>' due to: exit status 1
```
{: tsSymptoms}

Cela est très probablement dû à un nom de cluster non valide. Vous pouvez confirmer la cause de cette erreur en exécutant la même commande avec l'option `--trace`, qui permet d'afficher les détails suivants dans la sortie d'erreur : 

```
Failing with error:  {"incidentID":"<id-number>","code":"E0008","description":"The specified cluster could not be found.","recoveryCLI":"Run 'bx cs clusters' to list all clusters you have access to.","type":"Provisioning"}
```
{: tsCauses}

Assurez-vous que le cluster utilisé est correct et que vous l'avez bien configuré pour déploiement en exécutant la commande suivante : 

```
bx cs cluster-config <cluster-name>
```
{: tsResolve}

## Echec du déploiement d'une cible d'image

L'erreur suivante peut s'afficher après que vous avez indiqué la cible d'image de déploiement :

```
FAILED
Failed to execute the action:  exit status 1:denied: requested access to the resource is denied


FAILED
Failed to push the Run image tagged 'registry.ng.bluemix.net/<namespace>/<project-name>:0.0.1' to the Docker registry due to: exit status 1
```
{: tsSymptoms}

Cela est très probablement dû à une cible d'image de déploiement non valide. Plus spécifiquement, l'espace de nom, qui est la valeur du milieu dans la cible d'image de déploiement, n'est peut-être pas valide. 

Assurez-vous que l'espace de nom dans la cible d'image de déploiement correspond à l'un des espaces de nom trouvé à l'issue de l'exécution de la commande suivante : 

```
bx cr namespaces
```
{: tsResolve}
