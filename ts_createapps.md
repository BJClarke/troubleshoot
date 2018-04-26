---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-26"

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

# Troubleshooting for {{site.data.keyword.Bluemix_notm}} Developer Tools
{: #troubleshoot}

General problems with using the {{site.data.keyword.dev_cli_short}} to create apps might include deployment failures or code that can't be retrieved when creating a project. In many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}

## Hostname error when you create a project with a non-mobile pattern
{: #hostname-error}

You might see the following error if you use the {{site.data.keyword.dev_cli_short}} to create a project from the Web App, BFF, or Microservice patterns:

```
The hostname <myHostname> is taken.
```
{: codeblock}
{: tsSymptoms}

This error is caused by an expired login token.
{: tsCauses}

Log in again.

```
bx login
```
{: codeblock}
{: tsResolve}

## General failures with the {{site.data.keyword.dev_cli_short}}
{: #general}

You might see the following error if you use the {{site.data.keyword.dev_cli_short}} `create`, `delete`, `list`, or `code` commands:

```
Failed to <command> project.
```
{: codeblock}
{: tsSymptoms}

This error is caused by an expired login token.
{: tsCauses}

Log in again.

```
bx login
```
{: codeblock}
{: tsResolve}

## Error: No such image when you run a new project
{: #nosuchimage}

You might see the following error when you run a project without building it first.

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

You must build a project before you run it.
{: tsCauses}

Run the following command in your current project directory to build your application:

```
bx dev build
```
{: codeblock}

Run the following command in your current project directory to start your application:

```
bx dev run
```
{: tsResolve}

## Service broker error when you add the {{site.data.keyword.objectstorageshort}} capability
{: #os}

You might see the following error if you use the {{site.data.keyword.dev_cli_short}} to create two projects with the {{site.data.keyword.objectstorageshort}} capability:

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}
{: tsSymptoms}
   
This error is due to the {{site.data.keyword.objectstorageshort}} service, which provides only one instance of the free {{site.data.keyword.objectstorageshort}} plan.
{: tsCauses}

You are prompted to choose a different plan to avoid this error.
{: tsResolve}

## Failure getting the code when creating a project
{: #code}

You might see the following error if you use the {{site.data.keyword.dev_cli_short}} to create a project:
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
{: tsSymptoms}

This error is due to an internal timeout.
{: tsCauses}

You can get the code either of the following ways:

* Run the following command by using the CLI:

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   Replace `<your-project-name>` with the project name that you specified during project creation.

* Use the {{site.data.keyword.dev_console}}.

	1. Select your [project ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/developer/projects) in the {{site.data.keyword.dev_console}} and click **Get the Code**.

	2. Click **Generate Code**.

	3. After the code is generated, click **Download Code**.
{: tsResolve}

## Error running `bx dev run` for Node.js projects
{: #node}

You might see the following error if you are running `bx dev run` with the {{site.data.keyword.dev_cli_short}} for Node.js Web or BFF projects:

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
   
This error occurs when the `appmetrics` module is installed on a different architecture. Native npm modules that are installed on one architecture do not work on another. The included Docker images are based on the Linux kernel.
{: tsCauses}

Delete the `node_modules` folder and run the `bx dev run` command again.
{: tsResolve}

## Failure to deploy to {{site.data.keyword.Bluemix_notm}}

A failure occurs when you try deploying to {{site.data.keyword.Bluemix_notm}} with the {{site.data.keyword.dev_cli_short}}, but there is no error displayed.
{: tsSymptoms}

You might not be logged in to your account. 
{: tsCauses}

Log in and try again.

```
bx login
```
{: tsResolve}

## Failure to deploy to Kubernetes on {{site.data.keyword.Bluemix_notm}}

The following failure might be displayed after you're prompted for your cluster name:

```
FAILED
Failed to execute the action:  exit status 1:

FAILED
Failed to configure deployment with cluster '<cluster-name>' due to: exit status 1
```
{: tsSymptoms}

This is most likely due to a cluster name that's not valid. You can confirm the cause by running the same command with `--trace`, and the following details might be included in the error output:

```
Failing with error:  {"incidentID":"<id-number>","code":"E0008","description":"The specified cluster could not be found.","recoveryCLI":"Run 'bx cs clusters' to list all clusters you have access to.","type":"Provisioning"}
```
{: tsCauses}

Be sure that you are using the correct cluster and that you have configured your cluster for deployment by running: 

```
bx cs cluster-config <cluster-name>
```
{: tsResolve}

## Failure to deploy an image target

The following failure might be displayed after you're prompted for the deploy image target:

```
FAILED
Failed to execute the action:  exit status 1:denied: requested access to the resource is denied


FAILED
Failed to push the Run image tagged 'registry.ng.bluemix.net/<namespace>/<project-name>:0.0.1' to the Docker registry due to: exit status 1
```
{: tsSymptoms}

This is most likely due to a deploy image target that's not valid. More specifically, the namespace, which is the middle value in the deploy image target, might not be valid.

Be sure that the namespace in the deploy image target matches one of the namespaces found from running: 

```
bx cr namespaces
```
{: tsResolve}

## APPENDIX
{: #appendix}

All prerequisites install for most users using the platform installers. If you need to manually install any components, here are the instructions:

To install the dev plugin, you must first install the [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started).

To use the dev plugin itself, you must install it by running the following command: `bx plugin install dev -r Bluemix`

For running and debugging applications locally, you must also install [Docker](https://www.docker.com/get-docker).

For deploying an application as a container, you must also install Kubernetes, Helm, and the following IBM Cloud CLI plugins:

To install Kubernetes:
* Mac users:
`curl --progress-bar -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl`

* Linux users:
`curl --progress-bar -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl`

* Windows users:
`curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.7.0/bin/windows/amd64/kubectl.exe`

To install Helm:
* Mac and Linux users:
`export DESIRED_VERSION=v2.6.0`
`curl -sL https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash`

* Windows users:
Download and install the binary at https://github.com/kubernetes/helm/releases/tag/v2.6.0

To install the container-registry plugin:
`bx plugin install container-registry`

To install the container-service plugin:
`bx plugin install container-service`

