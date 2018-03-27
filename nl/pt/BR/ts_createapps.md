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

# Resolução de problemas para criar apps
{: #troubleshoot}

Os problemas gerais com o uso do {{site.data.keyword.dev_cli_short}} para criar apps podem incluir falhas de implementação ou código que não pode ser recuperado ao criar um projeto. Em muitos casos, é possível recuperar-se desses problemas seguindo algumas etapas simples.
{:shortdesc}

## Erro de nome do host quando você cria um projeto com um padrão não móvel
{: #hostname-error}

Será possível ver o erro a seguir se você usar a {{site.data.keyword.dev_cli_short}} para criar um projeto por meio dos padrões Web App, BFF ou Microservice:

```
The hostname <myHostname> is taken.
```
{: codeblock}
{: tsSymptoms}
   
Esse erro é causado por um token de login expirado.
{: tsCauses}

Efetue login novamente.

```
bx login
```
{: codeblock}
{: tsResolve}

## Falhas gerais com a {{site.data.keyword.dev_cli_short}}
{: #general}

Você poderá ver o erro a seguir se usar os comandos {{site.data.keyword.dev_cli_short}} `create`, `delete`, `list` ou `code`:

```
Failed to <command> project.
```
{: codeblock}
{: tsSymptoms}
   
Esse erro é causado por um token de login expirado.
{: tsCauses}

Efetue login novamente.

```
bx login
```
{: codeblock}
{: tsResolve}

## Erro: não há essa imagem ao executar um novo projeto
{: #nosuchimage}

O erro a seguir pode ser exibido ao executar um projeto sem construí-lo primeiro.

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

Deve-se construir um projeto antes de executá-lo. 
{: tsCauses}

Execute o comando a seguir no diretório de projeto atual para construir seu aplicativo:

```
bx dev build
```
{: codeblock}

Execute o comando a seguir no diretório de projeto atual para iniciar seu aplicativo:

```
bx dev run
```
{: tsResolve}

## Erro do broker de serviço ao incluir o recurso {{site.data.keyword.objectstorageshort}}
{: #os}

Será possível ver o erro a seguir se você usar a {{site.data.keyword.dev_cli_short}} para criar dois projetos com o recurso {{site.data.keyword.objectstorageshort}}:

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}
{: tsSymptoms}
   
Esse erro é devido ao serviço {{site.data.keyword.objectstorageshort}}, que fornece somente uma instância do plano grátis do {{site.data.keyword.objectstorageshort}}.
{: tsCauses}

É solicitado que você escolha um plano diferente para evitar esse erro.
{: tsResolve}

## Falha ao obter o código na criação de um projeto
{: #code}

Será possível ver o erro a seguir se você usar a {{site.data.keyword.dev_cli_short}} para criar um projeto:
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
{: tsSymptoms}

Esse erro deve-se a um tempo limite interno.
{: tsCauses}

É possível obter o código de uma das maneiras a seguir:

* Execute o comando a seguir usando a CLI:

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   Substitua `<your-project-name>` com o nome do projeto especificado durante a criação do projeto.

* Use o {{site.data.keyword.dev_console}}.

	1. Selecione seu [projeto ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/developer/projects) no {{site.data.keyword.dev_console}} e clique em **Obter o código**.

	2. Clique em **Gerar código**.

	3. Depois que o código for gerado, clique em **Fazer download do código**.
{: tsResolve}

## Erro ao executar `bx dev run` para projetos Node.js
{: #node}

Será possível ver o erro a seguir se você estiver executando `bx dev run` com a {{site.data.keyword.dev_cli_short}} para projetos Node.js Web ou BFF:

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
   
Esse erro ocorre quando o módulo `appmetrics` é instalado em uma arquitetura diferente. Módulos npm nativos que estão instalados em uma arquitetura não funcionam em outra. As imagens incluídas do Docker baseiam-se no kernel Linux.
{: tsCauses}

Exclua a pasta `node_modules` e execute o comando `bx dev run` novamente.
{: tsResolve}

## Falha ao implementar no {{site.data.keyword.Bluemix_notm}}

A falha ocorre quando você tenta implementar no {{site.data.keyword.Bluemix_notm}} com o {{site.data.keyword.dev_cli_short}}, mas não há erros exibidos.
{: tsSymptoms}

Você pode não estar com login efetuado em sua conta.
{: tsCauses}

Efetue login e tente novamente.

```
bx login
```
{: tsResolve}

## Falha ao implementar o Kubernetes no {{site.data.keyword.Bluemix_notm}}

A falha a seguir pode ser exibida após o nome do cluster ser solicitado:

```
FAILED
Falha ao executar a ação:  status de saída 1:

FAILED
Falha ao configurar a implementação com o cluster '<cluster-name>' devido a: status de saída 1
```
{: tsSymptoms}

Isso é mais provável devido a um nome de cluster que não é válido. É possível confirmar a causa executando o mesmo comando com `--trace` e os detalhes a seguir podem ser incluídos na saída de erro:

```
Falha com erro:  {"incidentID":"<id-number>","code":"E0008","description":"O cluster especificado não pôde ser localizado.","recoveryCLI":"Execute 'bx cs clusters' para listar todos os clusters aos quais você tem acesso.","type":"Fornecimento"}
```
{: tsCauses}

Para verificar se o cluster usado está correto e se você o configurou para implementação, execute: 

```
bx cs cluster-config <cluster-name>
```
{: tsResolve}

## Falha ao implementar um destino de imagem

A falha a seguir pode ser exibida após o destino de imagem de implementação ser solicitado:

```
FAILED
Falha ao executar a ação:  status de saída 1:denied: o acesso solicitado ao recurso foi negado


FAILED
Falha ao enviar por push a imagem de execução identificada como 'registry.ng.bluemix.net/<namespace>/<project-name>:0.0.1' para o registro do Docker devido a: status de saída 1
```
{: tsSymptoms}

Isso é mais provável devido a um destino de imagem de implementação que não é válido. Mais especificamente, o namespace, que é o valor médio no destino de imagem de implementação, pode não ser válido.

Verifique se o namespace no destino de imagem de implementação corresponde a um dos namespaces localizados na execução: 

```
bx cr namespaces
```
{: tsResolve}
