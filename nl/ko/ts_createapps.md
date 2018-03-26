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

# 앱 작성 문제점 해결
{: #troubleshoot}

앱 작성을 위해 {{site.data.keyword.dev_cli_short}}을 사용할 때 발생하는 일반 문제점에는 프로젝트를 작성할 때 검색되지 않는 코드나 배치 실패가 포함될 수 있습니다. 대부분 몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다.
{:shortdesc}

## 비-모바일 패턴이 있는 프로젝트를 작성할 때 호스트 오류
{: #hostname-error}

웹 앱, BFF 또는 마이크로서비스 패턴에서 프로젝트를 작성하기 위해 {{site.data.keyword.dev_cli_short}}을 사용하는 경우 다음 오류가 표시될 수 있습니다. 

```
The hostname <myHostname> is taken.
```
{: codeblock}
{: tsSymptoms}
   
이 오류는 로그인 토큰이 만료되어 발생합니다.
{: tsCauses}

다시 로그인하십시오. 

```
bx login
```
{: codeblock}
{: tsResolve}

## {{site.data.keyword.dev_cli_short}}의 일반 장애
{: #general}

{{site.data.keyword.dev_cli_short}} `create`, `delete`, `list` 또는 `code` 명령을 사용하는 경우 다음 오류가 표시될 수 있습니다. 

```
Failed to <command> project.
```
{: codeblock}
{: tsSymptoms}
   
이 오류는 로그인 토큰이 만료되어 발생합니다.
{: tsCauses}

다시 로그인하십시오. 

```
bx login
```
{: codeblock}
{: tsResolve}

## 오류: 새 프로젝트를 실행할 때 해당 이미지가 없음
{: #nosuchimage}

먼저 프로젝트를 빌드하지 않고 실행하면 다음 오류가 표시될 수 있습니다.

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

프로젝트를 실행하기 전에 먼저 빌드해야 합니다.
{: tsCauses}

애플리케이션을 빌드하려면 현재 프로젝트 디렉토리에서 다음 명령을 실행하십시오. 

```
bx dev build
```
{: codeblock}

애플리케이션을 시작하려면 현재 프로젝트 디렉토리에서 다음 명령을 실행하십시오. 

```
bx dev run
```
{: tsResolve}

## {{site.data.keyword.objectstorageshort}} 기능을 추가할 때 서비스 브로커 오류
{: #os}

{{site.data.keyword.objectstorageshort}} 기능으로 두 프로젝트를 작성하기 위해 {{site.data.keyword.dev_cli_short}}을 사용하는 경우 다음 오류가 표시될 수 있습니다. 

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}
{: tsSymptoms}
   
이 오류는 무료 {{site.data.keyword.objectstorageshort}} 사용제의 1개 인스턴스만 제공하는 {{site.data.keyword.objectstorageshort}} 서비스로 인한 것입니다.
{: tsCauses}

이 오류를 피하기 위해 다른 플랜을 선택하라는 프롬프트가 표시됩니다.
{: tsResolve}

## 프로젝트 작성 시 코드 가져오기 실패
{: #code}

프로젝트를 작성하기 위해 {{site.data.keyword.dev_cli_short}}을 사용하는 경우 다음 오류가 표시될 수 있습니다. 
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
{: tsSymptoms}

이 오류는 내부 제한시간 초과로 인한 것입니다.
{: tsCauses}

다음 방법 중 하나로 코드를 가져올 수 있습니다. 

* CLI를 사용하여 다음 명령을 실행하십시오. 

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   프로젝트 작성 동안 지정한 프로젝트 이름으로 `<your-project-name>`을 대체하십시오. 

* {{site.data.keyword.dev_console}}을 사용하십시오. 

	1. {{site.data.keyword.dev_console}}에서 [프로젝트 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.{DomainName}/developer/projects)를 선택한 다음 **코드 가져오기**를 클릭하십시오. 

	2. **코드 생성**을 클릭하십시오. 

	3. 코드가 생성되면 **코드 다운로드**를 클릭하십시오.
{: tsResolve}

## Node.js 프로젝트에 대해 `bx dev run` 실행 중 오류
{: #node}

Node.js 웹 또는 BFF 프로젝트에 대해 {{site.data.keyword.dev_cli_short}}으로 `bx dev run`을 실행하는 동안 다음 오류가 표시될 수 있습니다.

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
   
이 오류는 `appmetrics` 모듈이 다른 아키텍처에 설치될 때 발생할 수 있습니다. 한 아키텍처에 설치된 기본 npm 모듈은 다른 아키텍처에서 작동하지 않습니다. 포함된 Docker 이미지는 Linux 커널을 기반으로 합니다.
{: tsCauses}

`node_modules` 폴더를 삭제하고 `bx dev run` 명령을 다시 실행하십시오.
{: tsResolve}

## {{site.data.keyword.Bluemix_notm}}에 배치 실패

{{site.data.keyword.dev_cli_short}}으로 {{site.data.keyword.Bluemix_notm}}에 배치를 시도할 때 장애가 발생했지만 오류가 표시되지 않습니다.
{: tsSymptoms}

사용자의 계정에 로그인하지 못할 수도 있습니다.
{: tsCauses}

로그인하고 다시 시도하십시오.

```
bx login
```
{: tsResolve}

## {{site.data.keyword.Bluemix_notm}}에서 Kubernetes에 배치 실패

다음 장애는 클러스터 이름을 입력하라는 프롬프트가 표시된 후에 나타날 수 있습니다. 

```
FAILED
Failed to execute the action:  exit status 1:

FAILED
Failed to configure deployment with cluster '<cluster-name>' due to: exit status 1
```
{: tsSymptoms}

이는 올바르지 않은 클러스터 이름 때문일 가능성이 높습니다. 동일한 명령을 `--trace`와 함께 실행하여 원인을 확인할 수 있으며 다음 세부사항이 오류 출력에 포함될 수 있습니다. 

```
Failing with error:  {"incidentID":"<id-number>","code":"E0008","description":"The specified cluster could not be found.","recoveryCLI":"Run 'bx cs clusters' to list all clusters you have access to.","type":"Provisioning"}
```
{: tsCauses}

올바른 클러스터를 사용 중인지 확인하고 다음을 실행하여 배치에 대해 클러스터를 구성했는지 확인하십시오. 

```
bx cs cluster-config <cluster-name>
```
{: tsResolve}

## 이미지 대상을 배치하는 데 실패

다음 장애는 배치 이미지 대상을 입력하라는 프롬프트가 표시된 후에 나타날 수 있습니다. 

```
FAILED
Failed to execute the action:  exit status 1:denied: requested access to the resource is denied


FAILED
Failed to push the Run image tagged 'registry.ng.bluemix.net/<namespace>/<project-name>:0.0.1' to the Docker registry due to: exit status 1
```
{: tsSymptoms}

이는 올바르지 않은 배치 이미지 대상 때문일 가능성이 높습니다. 보다 구체적으로 배치 이미지 대상의 중간 값인 네임스페이스가 올바르지 않을 수 있습니다.

배치 이미지 대상의 네임스페이스가 다음을 실행하여 발견한 네임스페이스 중 하나와 일치하는지 확인하십시오. 

```
bx cr namespaces
```
{: tsResolve}
