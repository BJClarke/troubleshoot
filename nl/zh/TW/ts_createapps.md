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

# 建立應用程式的疑難排解
{: #troubleshoot}

使用 {{site.data.keyword.dev_cli_short}} 建立應用程式的一般問題可能包括部署失敗或建立專案時無法擷取的程式碼。在許多情況下，您可以遵照一些簡單的步驟，從這些問題回復。
{:shortdesc}

## 使用非行動型樣建立專案時發生主機名稱錯誤
{: #hostname-error}

如果您使用 {{site.data.keyword.dev_cli_short}} 從「Web 應用程式」、BFF 或「微服務」型樣建立專案，則可能會看到下列錯誤：

```
The hostname <myHostname> is taken.
```
{: codeblock}
{: tsSymptoms}
   
此錯誤是過期登入記號所造成。
{: tsCauses}

請重新登入。

```
bx login
```
{: codeblock}
{: tsResolve}

## {{site.data.keyword.dev_cli_short}} 的一般失敗
{: #general}

如果您使用 {{site.data.keyword.dev_cli_short}} `create`、`delete`、`list` 或 `code` 指令，則可能會看到下列錯誤：

```
Failed to <command> project.
```
{: codeblock}
{: tsSymptoms}
   
此錯誤是過期登入記號所造成。
{: tsCauses}

請重新登入。

```
bx login
```
{: codeblock}
{: tsResolve}

## 錯誤：當您執行新專案時，沒有這類映像檔
{: #nosuchimage}

當您執行專案而未先進行建置時，可能會看到下列錯誤。

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

您必須先建置專案，再執行專案。
{: tsCauses}

在現行專案目錄中執行下列指令，以建置您的應用程式：

```
bx dev build
```
{: codeblock}

在現行專案目錄中執行下列指令，以啟動您的應用程式：

```
bx dev run
```
{: tsResolve}

## 新增 {{site.data.keyword.objectstorageshort}} 功能時發生服務分配管理系統錯誤
{: #os}

如果您使用 {{site.data.keyword.dev_cli_short}} 建立兩個具有 {{site.data.keyword.objectstorageshort}} 功能的專案，則可能會看到下列錯誤：

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}
{: tsSymptoms}
   
此錯誤是 {{site.data.keyword.objectstorageshort}} 服務所造成，而此服務只提供免費 {{site.data.keyword.objectstorageshort}} 方案的一個實例。
{: tsCauses}

系統會提示您選擇不同的方案來避免此錯誤。
{: tsResolve}

## 建立專案時發生取得程式碼失敗
{: #code}

如果您使用 {{site.data.keyword.dev_cli_short}} 建立專案，則可能會看到下列錯誤：
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
{: tsSymptoms}

此錯誤是內部逾時所造成。
{: tsCauses}

您可以使用下列其中一種方式來取得程式碼：

* 使用 CLI 執行下列指令：

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   請將 `<your-project-name>` 取代為您在專案建立期間指定的專案名稱。

* 使用 {{site.data.keyword.dev_console}}。

	1. 在 {{site.data.keyword.dev_console}} 中選取[專案 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/developer/projects)，然後按一下**取得程式碼**。

	2. 按一下**產生程式碼**。

	3. 產生程式碼之後，請按一下**下載程式碼**。
{: tsResolve}

## 針對 Node.js 專案執行 `bx dev run` 時發生錯誤
{: #node}

如果您是搭配執行 `bx dev run` 與適用於 Node.js Web 或 BFF 專案的 {{site.data.keyword.dev_cli_short}}，則可能會看到下列錯誤：

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
   
`appmetrics` 模組安裝在不同的架構上時，會發生此錯誤。安裝在某個架構上的原生 mpm 模組無法在另一個架構上運作。所包括的 Docker 映像檔是以 Linux Kernel 為基礎。
{: tsCauses}

刪除 `node_modules` 資料夾，並重新執行 `bx dev run` 指令。
{: tsResolve}

## 無法部署至 {{site.data.keyword.Bluemix_notm}}

當您嘗試使用 {{site.data.keyword.dev_cli_short}} 部署至 {{site.data.keyword.Bluemix_notm}} 時失敗，但未顯示任何錯誤。
{: tsSymptoms}

您可能未登入您的帳戶。
{: tsCauses}

請登入，然後再試一次。

```
bx login
```
{: tsResolve}

## 無法部署至 {{site.data.keyword.Bluemix_notm}} 上的 Kubernetes

系統提示您輸入叢集名稱之後，可能會顯示下列失敗：

```
FAILED
Failed to execute the action:  exit status 1:

FAILED
Failed to configure deployment with cluster '<cluster-name>' due to: exit status 1
```
{: tsSymptoms}

這最可能是叢集名稱無效所造成。您可以執行與 `--trace` 相同的指令來確認原因，而錯誤輸出中可能會包含下列詳細資料：

```
Failing with error:  {"incidentID":"<id-number>","code":"E0008","description":"The specified cluster could not be found.","recoveryCLI":"Run 'bx cs clusters' to list all clusters you have access to.","type":"Provisioning"}
```
{: tsCauses}

請確定您使用的是正確叢集，而且您已透過執行下列指令來配置要進行部署的叢集： 

```
bx cs cluster-config <cluster-name>
```
{: tsResolve}

## 無法部署映像檔目標

系統提示您輸入部署映像檔目標之後，可能會顯示下列失敗：

```
FAILED
Failed to execute the action:  exit status 1:denied: requested access to the resource is denied


FAILED
Failed to push the Run image tagged 'registry.ng.bluemix.net/<namespace>/<project-name>:0.0.1' to the Docker registry due to: exit status 1
```
{: tsSymptoms}

這最可能是部署映像檔目標無效所造成。更具體來說，名稱空間（即部署映像檔目標中的中間值）可能無效。

請確定部署映像檔目標中的名稱空間符合執行下列指令所找到的其中一個名稱空間： 

```
bx cr namespaces
```
{: tsResolve}
