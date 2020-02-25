---
title: イベントモニター
kind: documentation
description: Datadog によって収集されたイベントを監視する
further_reading:
  - link: monitors/notifications
    tag: Documentation
    text: モニター通知の設定
  - link: monitors/downtimes
    tag: Documentation
    text: モニターをミュートするダウンタイムのスケジュール
  - link: monitors/monitor_status
    tag: Documentation
    text: モニターステータスを確認
---
## 概要

イベントモニターを使用すると、検索クエリと一致するイベントが発生したときにアラートを生成できます。

## モニターの作成

Datadog で[イベントモニター][1]を作成するには、メインナビゲーションで *Monitors --> New Monitor --> Metric* の順に移動します。

### カウントするイベントを選択する

下記のパラメーターを入力すると、検索フィールドの上にあるイベント一覧にフィルターがかかります。

* `<TEXT>` を含むイベントと一致
* ステータスが `error`、`warning`、`info` または `success`
* 優先度が `all`、`normal` または `low`
* 報告元 `<SOURCE>`
* 対象`<TAGS>`
* 除外 `<TAGS>`

アラートグループを選択します。

* **シンプルアラート**では、すべての報告元ソースを集計します。集計値が設定条件を満たすと、アラートを 1 件受信します。
* **マルチアラート**では、グループパラメーターに従って、ソースごとにアラートを適用します。設定条件を満たすと各グループにつき  1 件のアラートを受信します。

### アラートの条件を設定する

* カウントが `above`、`above or equal to`、`below`、または `below or equal to` の時
* `<THRESHOLD_NUMBER>`
* 期間は直前の `5 minutes`、`15 minutes`、`1 hour` など

**注**: 一部のプロバイダーでは、イベントが**ポスト**されてから実際に開始されるまでにかなりの遅延が生じます。このような場合、Datadog は発生時刻にまでさかのぼってイベントを記録しますが、これにより現在のモニター評価ウィンドウ外のイベントを認識することがあります。評価ウィンドウを広げると時間差が発生する原因を理解しやすくなります。適切なモニター設定の調整についてサポートが必要な場合は、[Datadog のサポートチーム][1]までお問い合わせください。

### 通知

**何が起きているのか**および**チームに通知**のセクションの詳細な手順については、[通知] [3]ページを参照してください。

#### イベントテンプレート変数

イベントモニターには、通知メッセージを入力できる特殊なテンプレート変数があります。

| テンプレート変数          | 定義                                                                     |
|----------------------------|--------------------------------------------------------------------------------|
| `{{event.id}}`             | イベントの ID。                                                           |
| `{{event.title}}`          | イベントのタイトル。                                                        |
| `{{event.text}}`           | イベントのテキスト。                                                         |
| `{{event.host.name}}`      | イベントを生成したホストの名前。                                 |
| `{{event.tags}}`           | イベントに関連したタグのリスト                                          |
| `{{event.tags.<TAG_KEY>}}` | イベントに関連した特定のタグキーの値。下記のサンプルを参照してください。 |

##### {{event.tags.&lt;TAG_KEY&gt;}}

次のタグ専用: `env:test`、`env:staging`、`env:prod`。

* `env` はタグキーです。
* `test`、`staging`、`prod` はタグ値です。

テンプレート変数は `{{event.tags.env}}` です。このテンプレート変数を使用した場合の結果は、`test`、`staging`、または `prod` です。

## その他の参考資料


{{< partial name="whats-next/whats-next.html" >}}

[1]: https://app.datadoghq.com/monitors#create/event
[2]: /ja/help
[3]: /ja/monitors/notifications