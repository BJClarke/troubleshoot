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

# Risoluzione dei problemi relativi alla creazione delle applicazioni 
{: #troubleshoot}

I problemi generali utilizzando {{site.data.keyword.dev_cli_short}} per creare le applicazioni potrebbero includere errori di distribuzione o del codice che non può essere richiamato quando crei un progetto. In molti casi, puoi risolvere questi problemi seguendo pochi semplici passi.
{:shortdesc}

## Errore nel nome host quando crei un progetto con un modello non mobile 
{: #hostname-error}

Potresti visualizzare il seguente errore se utilizzi la {{site.data.keyword.dev_cli_short}} per creare un progetto dai modelli applicazione web, BFF, o microservizio: 

```
The hostname <myHostname> is taken.
```
{: codeblock}
{: tsSymptoms}
   
Questo errore è causato da un token di accesso scaduto.
{: tsCauses}

Accedi nuovamente.

```
bx login
```
{: codeblock}
{: tsResolve}

## Errori generali con la {{site.data.keyword.dev_cli_short}} 
{: #general}

Potresti visualizzare il seguente errore se utilizzi la {{site.data.keyword.dev_cli_short}} con i comandi `create`, `delete`, `list` o `code`:

```
Failed to <command> project.
```
{: codeblock}
{: tsSymptoms}
   
Questo errore è causato da un token di accesso scaduto.
{: tsCauses}

Accedi nuovamente.

```
bx login
```
{: codeblock}
{: tsResolve}

## Errore: Nessuna immagine quando esegui un nuovo progetto 
{: #nosuchimage}

Potresti visualizzare il seguente errore quando esegui un progetto senza prima crearlo. 

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

Devi creare un progetto prima di eseguirlo.
{: tsCauses}

Immetti il seguente comando nella tua directory del progetto corrente per creare la tua applicazione:

```
bx dev build
```
{: codeblock}

Immetti il seguente comando nella tua directory del progetto corrente per avviare la tua applicazione:

```
bx dev run
```
{: tsResolve}

## Errore con il broker di servizi quando aggiungi la funzionalità {{site.data.keyword.objectstorageshort}} 
{: #os}

Potresti visualizzare il seguente errore se utilizzi la {{site.data.keyword.dev_cli_short}} per creare due progetti con la funzionalità {{site.data.keyword.objectstorageshort}}: 

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}
{: tsSymptoms}
   
Questo errore è dovuto al servizio {{site.data.keyword.objectstorageshort}} che fornisce solo un'istanza del piano {{site.data.keyword.objectstorageshort}} gratuito.
{: tsCauses}

Per evitare questo errore ti viene richiesto di scegliere un piano diverso.
{: tsResolve}

## Errore durante il richiamo del codice durante la creazione di un progetto 
{: #code}

Potresti visualizzare il seguente errore se utilizzi la {{site.data.keyword.dev_cli_short}} per creare un progetto: 
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
{: tsSymptoms}

Questo errore è dovuto a un timeout interno.
{: tsCauses}

Puoi ottenere il codice in uno dei seguenti modi: 

* Immetti il seguente comando utilizzando la CLI: 

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   Sostituisci `<your-project-name>` con il nome progetto che hai specificato durante la creazione del progetto. 

* Utilizza la {{site.data.keyword.dev_console}}.

	1. Seleziona il tuo progetto [ ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/developer/projects) nella {{site.data.keyword.dev_console}} e fai clic su **Ottieni codice**. 

	2. Fai clic su **Genera codice**. 

	3. Dopo aver generato il codice, fai clic su **Scarica codice**.
{: tsResolve}

## Errore durante l'esecuzione di `bx dev run` per i progetti Node.js 
{: #node}

Potresti visualizzare il seguente errore se stai eseguendo `bx dev run` con la {{site.data.keyword.dev_cli_short}} per i progetti Node.js Web o BFF: 

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
   
Questo errore si verifica quando il modulo `appmetrics` viene installato su un'architettura diversa. I moduli npm nativi installati su un'architettura non funzionano su un'altra. Le immagini Docker incluse si basano sul kernel Linux.
{: tsCauses}

Elimina la cartella `node_modules` ed esegui nuovamente il comando `bx dev run`.
{: tsResolve}

## Impossibile distribuire a {{site.data.keyword.Bluemix_notm}}

Si è verificato un errore durante la distribuzione a {{site.data.keyword.Bluemix_notm}} con la {{site.data.keyword.dev_cli_short}}, ma non viene visualizzato alcun errore.
{: tsSymptoms}

Potresti non essere collegato al tuo account.
{: tsCauses}

Effettua l'accesso e riprova.

```
bx login
```
{: tsResolve}

## Impossibile distribuire a Kubernetes in {{site.data.keyword.Bluemix_notm}}

Il seguente errore potrebbe essere visualizzato dopo che ti viene richiesto il tuo nome del cluster: 

```
FAILED
Failed to execute the action:  exit status 1:

FAILED
Failed to configure deployment with cluster '<cluster-name>' due to: exit status 1
```
{: tsSymptoms}

Molto probabilmente è causato da un nome del cluster non valido. Puoi confermare la causa eseguendo lo stesso comando con `--trace` e i seguenti dettagli potrebbero essere inclusi nell'output dell'errore:

```
Failing with error:  {"incidentID":"<id-number>","code":"E0008","description":"The specified cluster could not be found.","recoveryCLI":"Run 'bx cs clusters' to list all clusters you have access to.","type":"Provisioning"}
```
{: tsCauses}

Assicurati di stare utilizzando il cluster corretto e di aver configurato il tuo cluster per la distribuzione eseguendo: 

```
bx cs cluster-config <cluster-name>
```
{: tsResolve}

## Impossibile distribuire a una destinazione dell'immagine 

Il seguente errore potrebbe essere visualizzato dopo che ti viene richiesta la destinazione dell'immagine da distribuire: 

```
FAILED
Failed to execute the action:  exit status 1:denied: requested access to the resource is denied


FAILED
Failed to push the Run image tagged 'registry.ng.bluemix.net/<namespace>/<project-name>:0.0.1' to the Docker registry due to: exit status 1
```
{: tsSymptoms}

Molto probabilmente è causato da una destinazione dell'immagine da distribuire non valida. Nello specifico, lo spazio dei nomi, che è il valore medio nella destinazione dell'immagine da distribuire, potrebbe non essere valido.

Assicurati che lo spazio dei nomi nella destinazione dell'immagine da distribuire corrisponda a uno degli spazi dei nomi trovati dall'esecuzione:  

```
bx cr namespaces
```
{: tsResolve}
