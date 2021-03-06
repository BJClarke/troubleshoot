---

copyright:

  years: 2015, 2018

lastupdated: "2016-08-12"


---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}


# 一般的なサービスの問題
{: #general}

{{site.data.keyword.Bluemix}} サービスの問題には、ユーザーがサービス・インスタンスを削除した場合に発生するゲートウェイ・タイムアウト・エラーなどが含まれます。 しかし多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}

## サービス・インスタンスの削除時にサービス・ブローカー・エラーが発生する
{: #ts_service_broker}

クラウド・コントローラーから既に削除されたサービス・インスタンスを削除しようとすると、エラー・メッセージが表示されます。
{:shortdesc}


サービス・インスタンスを削除しようとすると、`「ゲートウェイ・タイムアウト (Gateway timeout)」`というサービス・ブローカーのエラー・メッセージが表示されます。
{: tsSymptoms}


この問題は、そのサービス・インスタンスが既にクラウド・コントローラーから削除済みである場合に発生します。
{: tsCauses}


この問題を解決するには、同じサービス名でサービス・インスタンスを作成し、それをアプリケーションにバインドします。 その後、そのサービス・インスタンスとそのサービスを使用するアプリケーションを削除することができます。   
{: tsResolve}
