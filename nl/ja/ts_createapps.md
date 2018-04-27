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

# アプリの作成に関するトラブルシューティング
{: #troubleshoot}

{{site.data.keyword.dev_cli_short}} を使用してアプリを作成する際の一般的な問題には、デプロイメントの失敗や、プロジェクトを作成する際にコードを取得できないなどが含まれます。 多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}

## 非モバイル・パターンのプロジェクトを作成するとホスト名エラーになる
{: #hostname-error}

{{site.data.keyword.dev_cli_short}} を使用して、Web アプリ・パターン、BFF パターン、またはマイクロサービス・パターンからプロジェクトを作成すると、以下のエラーが表示される場合があります。

```
The hostname <myHostname> is taken.
```
{: codeblock}
{: tsSymptoms}
   
このエラーの原因は、ログイン・トークンが有効期限切れになったことです。
{: tsCauses}

再ログインしてください。

```
bx login
```
{: codeblock}
{: tsResolve}

## {{site.data.keyword.dev_cli_short}} の一般障害
{: #general}

{{site.data.keyword.dev_cli_short}} の `create`、`delete`、 `list`、または `code` のコマンドを使用すると、以下のエラーが表示される場合があります。

```
Failed to <command> project.
```
{: codeblock}
{: tsSymptoms}
   
このエラーの原因は、ログイン・トークンが有効期限切れになったことです。
{: tsCauses}

再ログインしてください。

```
bx login
```
{: codeblock}
{: tsResolve}

## エラー: 新規プロジェクトを実行すると、「No such image」と表示される
{: #nosuchimage}

ビルドをせずにプロジェクトを実行すると、以下のエラーが表示される場合があります。

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

プロジェクトは、実行する前にビルドする必要があります。 
{: tsCauses}

現行プロジェクト・ディレクトリー内で以下のコマンドを実行して、アプリケーションをビルドします。

```
bx dev build
```
{: codeblock}

現行プロジェクト・ディレクトリー内で以下のコマンドを実行して、アプリケーションを開始します。

```
bx dev run
```
{: tsResolve}

## {{site.data.keyword.objectstorageshort}} 機能を追加すると、サービス・ブローカー・エラーが発生する
{: #os}

{{site.data.keyword.dev_cli_short}} を使用して、{{site.data.keyword.objectstorageshort}} 機能を持つ 2 つのプロジェクトを作成すると、以下のエラーが表示される場合があります。

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}
{: tsSymptoms}
   
このエラーの原因は、{{site.data.keyword.objectstorageshort}} サービスが、フリー {{site.data.keyword.objectstorageshort}} プランの 1 つのインスタンスのみ提供していることです。
{: tsCauses}

このエラーを回避するために、別のプランを選択するようプロンプトが出されます。
{: tsResolve}

## プロジェクトの作成時にコードの取得に失敗する
{: #code}

{{site.data.keyword.dev_cli_short}} を使用してプロジェクトを作成すると、以下のエラーが表示される場合があります。
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
{: tsSymptoms}

このエラーの原因は、内部タイムアウトです。
{: tsCauses}

以下のいずれかの方法でコードを取得できます。

* CLI を使用して以下のコマンドを実行します。

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   `<your-project-name>` を、プロジェクト作成時に指定したプロジェクト名で置き換えます。

* {{site.data.keyword.dev_console}}を使用します。

	1. {{site.data.keyword.dev_console}}で、[プロジェクト![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.{DomainName}/developer/projects)を選択し、**「コードの取得 (Get the Code)」**をクリックします。

	2. **「コードの生成 (Generate Code)」**をクリックします。

	3. コードの生成が終了したら、**「コードのダウンロード」**をクリックします。
{: tsResolve}

## Node.js プロジェクトで `bx dev run` を実行するとエラーになる
{: #node}

Node.js Web プロジェクトまたは BFF プロジェクト用の {{site.data.keyword.dev_cli_short}} で `bx dev run` を実行すると、以下のエラーが表示される場合があります。

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
   
このエラーは、`appmetrics` モジュールが別のアーキテクチャーにインストールされている場合に発生します。 1 つのアーキテクチャーにインストールされているネイティブ NPM モジュールは、別のアーキテクチャーでは機能しません。 付属の Docker イメージは、Linux カーネルに基づいています。
{: tsCauses}

`node_modules` フォルダーを削除してから、`bx dev run` コマンドを再度実行します。
{: tsResolve}

## {{site.data.keyword.Bluemix_notm}} へのデプロイに失敗する

{{site.data.keyword.dev_cli_short}} を使用して {{site.data.keyword.Bluemix_notm}} へデプロイしようとすると、失敗しますが、エラーは表示されません。
{: tsSymptoms}

アカウントにログインしていない可能性があります。 
{: tsCauses}

ログインして、やり直してください。

```
bx login
```
{: tsResolve}

## {{site.data.keyword.Bluemix_notm}} 上の Kubernetes へのデプロイに失敗する

クラスター名のプロンプトが出された後、以下の失敗が表示される場合があります。

```
FAILED
Failed to execute the action:  exit status 1:

FAILED
Failed to configure deployment with cluster '<cluster-name>' due to: exit status 1
```
{: tsSymptoms}

これは、ほとんどの場合、無効のクラスター名が原因です。 同じコマンドに `--trace` を付けて実行することによって、原因を確認することができます。エラー出力には、以下の詳細が含まれる場合があります。

```
Failing with error:  {"incidentID":"<id-number>","code":"E0008","description":"The specified cluster could not be found.","recoveryCLI":"Run 'bx cs clusters' to list all clusters you have access to.","type":"Provisioning"}
```
{: tsCauses}

正しいクラスターを使用していて、かつクラスターがデプロイメント用に構成済みであることを確認するために、以下を実行します。 

```
bx cs cluster-config <cluster-name>
```
{: tsResolve}

## イメージ・ターゲットのデプロイに失敗する

デプロイ用イメージ・ターゲットのプロンプトが出された後、以下の失敗が表示される場合があります。

```
FAILED
Failed to execute the action:  exit status 1:denied: requested access to the resource is denied


FAILED
Failed to push the Run image tagged 'registry.ng.bluemix.net/<namespace>/<project-name>:0.0.1' to the Docker registry due to: exit status 1
```
{: tsSymptoms}

これは、ほとんどの場合、無効のデプロイ用イメージ・ターゲットが原因です。 具体的には、デプロイ用イメージ・ターゲットの中間値である名前空間が無効である可能性があります。

デプロイ用イメージ・ターゲット内の名前空間が、以下を実行して表示される名前空間のいずれかと一致していることを確認します。 

```
bx cr namespaces
```
{: tsResolve}
