---

copyright:

  years: 2018

lastupdated: "2018-05-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# クイック・スタート・テンプレートのデプロイ
{: #serviceauth}

{{site.data.keyword.openwhisk}} は、次のプロジェクトを迅速に開始できるように、テンプレートのカタログを提供します。 テンプレートは、アクション、トリガー、シーケンスの組み合わせであり、{{site.data.keyword.Bluemix}} からのサービス・インスタンスを取り込むこともできます。 テンプレートを使用することで、プロジェクトを迅速かつ簡単に作成し、直ちにコーディングを開始できます。

このチュートリアルでは、Cloudant テンプレートのデプロイについて順に説明します。
{: shortdesc}

## 使用可能なクイック・スタート・テンプレート
{: #available-templates}

| 名前 | 説明 | サポートされるランタイム |
|:-----------------|:-----------------|:-----------------|
| [Cloudant Events](./deploy_templates.html#cloudant-template) | Cloudant DB で文書が編集または追加された場合に、コンソールに変更を出力します。 | Node.js、Swift、Python、PHP |
| [Get HTTP Resource](./deploy_templates.html#get-http-resource-template) | HTTP イベントに対する応答として呼び出され、Yahoo Weather API からデータをフェッチする Web アクション。 | Node.js、Python |
| [Hello World](./deploy_templates.html#hello-world-template) | このアクションは 1 つのパラメーターを受け入れます。このパラメーターは JSON オブジェクトでなければなりません。 | Node.js、Swift、Python、PHP |
| [Message Hub Events](./deploy_templates.html#messagehub-events-template) | メッセージ・ハブ・トピックで新しいデータが追加されると、コンソールに変更を出力します。 | Node.js、Swift、Python、PHP |
| [Periodic Slack Reminder](./deploy_templates.html#slack-reminder-template) | 定期的なトリガーに基づいて、Slack に投稿するアクション。 | Node.js、Swift、Python、PHP |

## Cloudant Events テンプレートのデプロイ
{: #cloudant-template}

Cloudant テンプレートは、アクション・シーケンス、およびそのシーケンスを開始するトリガーを作成します。 トリガーは、接続されている Cloudant DB で変更が生じると起動します。この DB は、名前と色を持つ猫のデータベースです。 予期されるデータ項目は猫であり、名前と色が定義されています。 新しい猫がデータベースに追加されるか、現在の猫が編集されると、データがコンソールに出力されます。

1. テンプレートを作成するには、[{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.openwhisk_short}}](https://console.bluemix.net/openwhisk/) に移動してから、**「作成の開始」**をクリックします。

2. **「クイック・スタート・テンプレート (Quickstart Templates)」**をクリックします。

3. **「新規 Cloudant 項目 (New Cloudant Item)」**をクリックします。

### Cloudant アクションの作成

1. 次に、パッケージの名前を指定するか、提供されているデフォルト名 `new-cloudant-item` を使用します。

2. **「アクション」**ドロップダウンの下で、所有するアクションのランタイム (nodejs、swift、python、または php) を選択します。 この例では、**「nodejs」**を選択し、**「次へ」**をクリックします。

### Cloudant トリガーの作成

トリガーは、イベント・ソースからイベントを受信するとアクションを呼び出します。 Cloudant テンプレート用のトリガーを作成するには、トリガーに対し、必要な Cloudant サービス・インスタンス情報を指定します。

#### Cloudant サービス・インスタンスの作成

以下のいずれかの操作から選択できます。
  * **独自のインスタンスの作成**
  * **独自の資格情報の入力**

1. この例では、**独自のインスタンスの作成**を選択します。

2. ポップアップが開き、Cloudant セットアップ・ページが含まれた新規タブが表示されます。 Cloudant インスタンスを作成した後に、サービス資格情報セットを作成してから、**「OK」**をクリックしてタブを閉じてこのページに戻る必要があります。

3. 次に、**独自の資格情報の入力**を選択し、以下の情報を指定します。
  * ユーザー名 - _Cloudant ユーザー名_
  * パスワード - _Cloudant パスワード_
  * ホスト - _これは通常、`username.cloudant.com`_
  * データベース - _Cloudant データベースの名前_

### Cloudant テンプレートのデプロイ

**「デプロイ」**をクリックします。

テンプレートのデプロイ後、必要に応じてカスタマイズするためにさらにコードを編集するか、戻って使用可能なテンプレートのカタログを確認できます。

## Get HTTP Resource テンプレートのデプロイ
{: #get-http-resource-template}

Get HTTP Resource テンプレートは、外部リソースである Yahoo Weather API をフェッチするためのアクションを作成し、その後、データを返します。アクションは Web アクションとして有効にされるので、CORS 対応の URL を使用して呼び出すことが可能で、認証鍵は必要ありません。これは、Web アプリケーションのバックエンドを構築するのに役立ちます。**注**: デフォルトでは、`get-http-resource` エンドポイントは、このエンドポイントを呼び出すことができるあらゆるユーザーに対して公開されています。

1. テンプレートを作成するには、[{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.openwhisk_short}}](https://console.bluemix.net/openwhisk/) に移動してから、**「作成の開始」**をクリックします。

2. **「クイック・スタート・テンプレート (Quickstart Templates)」**をクリックします。

3. **「パッケージ名」**フィールドを確認します。このフィールドは必要に応じて更新できます。デフォルトでは、`get-http-resource` と設定されます。

4. 所有するアクションのランタイムを選択します。Node.js 8、Node.js 6、または Python 3 のいずれかです。

5. **「デプロイ」**をクリックします。

テンプレートのデプロイ後、必要に応じてカスタマイズするためにさらにコードを編集するか、戻って使用可能なテンプレートのカタログを確認できます。

## Hello World テンプレートのデプロイ
{: #hello-world-template}

このアクションは 1 つのパラメーターを受け入れます。このパラメーターは JSON オブジェクトでなければなりません。

1. テンプレートを作成するには、[{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.openwhisk_short}}](https://console.bluemix.net/openwhisk/) に移動してから、**「作成の開始」**をクリックします。

2. **「クイック・スタート・テンプレート (Quickstart Templates)」**をクリックします。

3. **「パッケージ名」**フィールドを確認します。このフィールドは必要に応じて更新できます。デフォルトでは、`hello-world` と設定されます。

4. 所有するアクションのランタイムを選択します。Node.js 8、Node.js 6、Python 3、Swift 4、または PHP 7.1 のいずれかです。

5. **「デプロイ」**をクリックします。

テンプレートのデプロイ後、必要に応じてカスタマイズするためにさらにコードを編集するか、戻って使用可能なテンプレートのカタログを確認できます。

## Message Hub Events テンプレートのデプロイ
{: #messagehub-events-template}

Message Hub Events テンプレートは、アクションおよびそのアクションを開始するトリガーを作成します。テンプレートの作成時に選択された Message Hub トピックに新しい項目が追加されるたびにトリガーが起動されます。

1. テンプレートを作成するには、[{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.openwhisk_short}}](https://console.bluemix.net/openwhisk/) に移動してから、**「作成の開始」**をクリックします。

2. **「クイック・スタート・テンプレート (Quickstart Templates)」**をクリックします。

3. **「パッケージ名」**フィールドを確認します。このフィールドは必要に応じて更新できます。デフォルトでは、`message-hub-events` と設定されます。

4. 所有するアクションのランタイムを選択します。Node.js 8、Node.js 6、Python 3、Swift 4、または PHP 7.1 のいずれかです。

5. **「次へ」**をクリックします。

### Message Hub トリガーの作成

トリガーは、イベント・ソースからイベントを受信するとアクションを呼び出します。 Message Hub テンプレート用のトリガーを作成するには、トリガーに対し、必要な Message Hub サービス・インスタンス情報を指定します。

**「トリガー名」**フィールドを確認します。このフィールドは必要に応じて更新できます。デフォルトでは、`message-hub-events-trgr` と設定されます。

### Message Hub サービス・インスタンスの作成

以下のいずれかの操作から選択できます。
  * **独自のインスタンスの作成**
  * **独自の資格情報の入力**

1. この例では、**独自のインスタンスの作成**を選択します。

2. ポップアップが開き、Message Hub セットアップ・ページが含まれた新規タブが表示されます。 Message Hub インスタンスを作成した後に、サービス資格情報セットを作成してから、**「OK」**をクリックしてタブを閉じてこのページに戻る必要があります。

3. 次に、**独自の資格情報の入力**を選択し、以下の情報を指定します。
  * ユーザー名 - _Message Hub ユーザー名_
  * パスワード - _Message Hub パスワード_
  * kafka_admin_url - _Message Hub 管理 REST URL_
  * データベース - _Message Hub データベースの名前_
  * トピック - _サブスクライブするトピック_

### Message Hub テンプレートのデプロイ

**「デプロイ」**をクリックします。

テンプレートのデプロイ後、必要に応じてカスタマイズするためにさらにコードを編集するか、戻って使用可能なテンプレートのカタログを確認できます。

## Periodic Slack Reminder テンプレートのデプロイ
{: #slack-reminder-template}

Periodic Slack Reminder テンプレートは、トリガー作成時にユーザーによって指定された間隔で Slack に通知します。このテンプレートを作成する前に、https://api.slack.com/incoming-webhooks にアクセスして、必要な着信 Webhook URL をセットアップしてください。

1. **「パッケージ名」**フィールドを確認します。このフィールドは必要に応じて更新できます。デフォルトでは、`periodic-slack-reminder` と設定されます。

2. 所有するアクションのランタイムを選択します。Node.js 8、Node.js 6、Python 3、Swift 4、または PHP 7.1 のいずれかです。

3. **「パラメーター」**セクションで、**「パラメーター値」**フィールドに Webhook URL を入力し、**「次へ」**をクリックします。(例: https://hooks.slack.com/TXXXXX/BXXXXX/XXXXXXXXXX)

### Slack Reminder トリガーの作成

トリガーは、イベント・ソースからイベントを受信するとアクションを呼び出します。 Slack Reminder テンプレート用のトリガーを作成するには、トリガーに対し、必要な Message Hub サービス・インスタンス情報を指定します。

1. **「トリガー名」**フィールドを確認します。このフィールドは必要に応じて更新できます。デフォルトでは、`periodic-slack-reminder-trgr` と設定されます。

2. 次に、パターンまたはクーロン式を使用して、トリガーを起動する間隔を指定できます。平日、時間、および分に応じた UTC 時刻を選択できます。希望する間隔オプションを選択すると、テンプレートのデプロイメントの準備ができます。

3. **「デプロイ」**をクリックします。

テンプレートのデプロイ後、必要に応じてカスタマイズするためにさらにコードを編集するか、戻って使用可能なテンプレートのカタログを確認できます。
