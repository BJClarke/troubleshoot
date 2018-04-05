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

# Fehlerbehebung für die Erstellung von Apps
{: #troubleshoot}

Allgemeine Probleme bei Verwendung der {{site.data.keyword.dev_cli_short}} zum Erstellen von Apps sind beispielsweise Bereitstellungsfehler oder Code, der beim Erstellen eines Projekts nicht abgerufen werden kann. In vielen Fällen können Sie diese Probleme durch Ausführen weniger einfacher Schritte beheben.
{:shortdesc}

## Hostnamenfehler beim Erstellen eines Projekts mit einem nicht mobilen Muster
{: #hostname-error}

Möglicherweise wird der folgende Fehler ausgegeben, wenn Sie die {{site.data.keyword.dev_cli_short}} verwenden, um ein Projekt aus den Web-App-, BFF- oder Mikroservice-Mustern zu erstellen: 

```
The hostname <myHostname> is taken.
```
{: codeblock}
{: tsSymptoms}
   
Dieser Fehler wird durch ein abgelaufenes Anmeldetoken verursacht.
{: tsCauses}

Melden Sie sich erneut an. 

```
bx login
```
{: codeblock}
{: tsResolve}

## Allgemeine Fehler mit der {{site.data.keyword.dev_cli_short}}
{: #general}

Möglicherweise wird der folgende Fehler ausgegeben, wenn Sie die Befehle {{site.data.keyword.dev_cli_short}} `create`, `delete`, `list` oder `code` verwenden: 

```
Failed to <command> project.
```
{: codeblock}
{: tsSymptoms}
   
Dieser Fehler wird durch ein abgelaufenes Anmeldetoken verursacht.
{: tsCauses}

Melden Sie sich erneut an. 

```
bx login
```
{: codeblock}
{: tsResolve}

## Fehler 'No such image', wenn Sie ein neues Projekt ausführen
{: #nosuchimage}

Möglicherweise wird der folgende Fehler angezeigt, wenn Sie ein Projekt ausführen, ohne es zunächst zu erstellen. 

```
$ bx dev run testProject
The run-cmd option was not specified
Stopping the 'testProject' container...
The 'testProject' container was not found
Creating image bx-dev-testProject based on Dockerfile...
OK                    
Creating a container named 'testProject' from that image...
FAILED
Container 'testProject' could not be created:
Error: No such image: bx-dev-testProject
```
{: tsSymptoms}

Sie müssen ein Projekt erstellen, bevor Sie es ausführen.
{: tsCauses}

Führen Sie den folgenden Befehl in Ihrem aktuellen Projektverzeichnis aus, um Ihre Anwendung zu erstellen: 

```
bx dev build
```
{: codeblock}

Führen Sie den folgenden Befehl in Ihrem aktuellen Projektverzeichnis aus, um Ihre Anwendung zu starten: 

```
bx dev run
```
{: tsResolve}

## Service-Broker-Fehler beim Hinzufügen der {{site.data.keyword.objectstorageshort}}-Funktionalität
{: #os}

Möglicherweise wird der folgende Fehler angezeigt, wenn Sie die {{site.data.keyword.dev_cli_short}} verwenden, um zwei Projekte mit der {{site.data.keyword.objectstorageshort}}-Funktionalität zu erstellen: 

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}
{: tsSymptoms}
   
Dieser Fehler wird vom {{site.data.keyword.objectstorageshort}}-Service verursacht, der nur eine Instanz des freien {{site.data.keyword.objectstorageshort}}-Plans bereitstellen kann.
{: tsCauses}

Sie werden aufgefordert, einen anderen Plan auszuwählen, um diesen Fehler zu vermeiden.
{: tsResolve}

## Fehler beim Abrufen des Codes während der Erstellung eines Projekts
{: #code}

Möglicherweise wird der folgende Fehler ausgegeben, wenn Sie die {{site.data.keyword.dev_cli_short}} verwenden, um ein Projekt zu erstellen: 
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
{: tsSymptoms}

Dieser Fehler wird durch eine interne Zeitlimitüberschreitung verursacht.
{: tsCauses}

Sie können den Code auf eine der folgenden Arten abrufen: 

* Führen Sie den folgenden Befehl in der CLI aus: 

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   Ersetzen Sie `<your-project-name>` durch den Namen des Projekts, das Sie während der Projekterstellung angegeben haben. 

* Öffnen Sie die {{site.data.keyword.dev_console}}. 

	1. Wählen Sie Ihr [Projekt ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/developer/projects) in der {{site.data.keyword.dev_console}} aus und klicken Sie auf **Code abrufen**. 

	2. Klicken Sie auf **Code generieren**. 

	3. Klicken Sie auf **Code herunterladen**, nachdem der Code generiert wurde.
{: tsResolve}

## Fehler beim Ausführen von `bx dev run` für Node.js-Projekte
{: #node}

Möglicherweise wird der folgende Fehler ausgegeben, wenn Sie `bx dev run` in der {{site.data.keyword.dev_cli_short}} für Web- oder BFF-Projekte mit Node.js ausführen: 

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
   
Dieser Fehler tritt auf, wenn das Modul `appmetrics` in einer anderen Architektur installiert ist. Native NPM-Module, die in einer Architektur installiert sind, funktionieren nicht in einer anderen. Die eingeschlossenen Docker-Images basieren auf dem Linux-Kernel.
{: tsCauses}

Löschen Sie den Ordner `node_modules` und führen Sie den Befehl `bx dev run` erneut aus.
{: tsResolve}

## Fehler bei der Bereitstellung in {{site.data.keyword.Bluemix_notm}}

Es tritt ein Fehler auf, wenn Sie die Bereitstellung in {{site.data.keyword.Bluemix_notm}} über die {{site.data.keyword.dev_cli_short}} versuchen, aber es wird kein Fehler angezeigt.
{: tsSymptoms}

Möglicherweise sind Sie nicht bei Ihrem Konto angemeldet.
{: tsCauses}

Melden Sie sich an und versuchen Sie es erneut.

```
bx login
```
{: tsResolve}

## Fehler bei der Bereitstellung in Kubernetes unter {{site.data.keyword.Bluemix_notm}}

Möglicherweise wird der folgende Fehler angezeigt, nachdem Sie aufgefordert wurden, Ihren Clusternamen anzugeben. 

```
FAILED
Failed to execute the action:  exit status 1:

FAILED
Failed to configure deployment with cluster '<cluster-name>' due to: exit status 1
```
{: tsSymptoms}

Dies liegt wahrscheinlich daran, dass der Clustername nicht gültig ist. Bestätigen Sie diese Annahme, indem Sie denselben Befehl mit `--trace` ausführen. Die folgenden Details können in der Fehlernachricht enthalten sein: 

```
Failing with error:  {"incidentID":"<id-number>","code":"E0008","description":"The specified cluster could not be found.","recoveryCLI":"Run 'bx cs clusters' to list all clusters you have access to.","type":"Provisioning"}
```
{: tsCauses}

Stellen Sie sicher, dass Sie den korrekten Cluster verwenden und dass Sie Ihren Cluster für die Bereitstellung konfiguriert haben, indem Sie den folgenden Befehl ausführen:  

```
bx cs cluster-config <cluster-name>
```
{: tsResolve}

## Fehler bei der Bereitstellung eines Imageziels

Möglicherweise wird der folgende Fehler angezeigt, nachdem Sie zur Angabe des Bereitstellungsimageziels aufgefordert wurden: 

```
FAILED
Failed to execute the action:  exit status 1:denied: requested access to the resource is denied


FAILED
Failed to push the Run image tagged 'registry.ng.bluemix.net/<namespace>/<project-name>:0.0.1' to the Docker registry due to: exit status 1
```
{: tsSymptoms}

Dies liegt wahrscheinlich daran, dass das Bereitstellungsimageziel nicht gültig ist. Genauer gesagt, ist wahrscheinlich der Namensbereich, bei dem es sich um den mittleren Wert im Bereitstellungsimageziel handelt, nicht gültig. 

Stellen Sie sicher, dass der Namensbereich im Bereitstellungsimageziel einem der Namensbereiche entspricht, die während der Ausführung des folgenden Befehls gefunden werden:  

```
bx cr namespaces
```
{: tsResolve}
