`shortcut()` メソッドは、[グローバルショートカット](https://api.slack.com/interactivity/shortcuts/using#global_shortcuts)と[メッセージショートカット](https://api.slack.com/interactivity/shortcuts/using#message_shortcuts)の両方をサポートします。

ショートカットは、テキスト入力エリアや検索バーから起動できる Slack クライアント内の UI エレメントです。グローバルショートカットは、コンポーザーメニューまたは検索メニューから呼び出すことができます。メッセージショートカットは、メッセージのコンテキストメニュー内にあります。`shortcut()` メソッドを使って、これらのショートカットのイベントをリッスンすることができます。このメソッドには `callback_id` を文字列または正規表現のデータ型で設定します。

グローバルショートカットのイベントは Slack へイベントを受信したことを知らせるために `ack()` メソッドで確認する必要があります。

グローバルショートカットのペイロードは、ユーザーの実行アクションの確認のために[モーダルを開く](#creating-modals)などの用途に使用できる `trigger_id` を含んでいます。

⚠️ グローバルショートカットのペイロードは **チャンネル ID は含んでいない** ことに注意してください。もしあなたのアプリがチャンネル ID を知る必要があれば、モーダル内で [`conversations_select`](https://api.slack.com/reference/block-kit/block-elements#conversation_select) エレメントを使用できます。
メッセージショートカットのペイロードはチャンネル ID を含みます。

```javascript
// open_modal というグローバルショートカットはシンプルなモーダルを開く
app.shortcut('open_modal', async ({ shortcut, ack, context }) => {
  // グローバルショートカットリクエストの確認
  ack();

  try {
    // 組み込みの WebClient を使って views.open API メソッドを呼び出す
    const result = await app.client.views.open({
      // `context` オブジェクトに保持されたトークンを使用
      token: context.botToken,
      trigger_id: shortcut.trigger_id,
      view: {
        "type": "modal",
        "title": {
          "type": "plain_text",
          "text": "My App"
        },
        "close": {
          "type": "plain_text",
          "text": "Close"
        },
        "blocks": [
          {
            "type": "section",
            "text": {
              "type": "mrkdwn",
              "text": "About the simplest modal you could conceive of :smile:\n\nMaybe <https://api.slack.com/reference/block-kit/interactive-components|*make the modal interactive*> or <https://api.slack.com/surfaces/modals/using#modifying|*learn more advanced modal use cases*>."
            }
          },
          {
            "type": "context",
            "elements": [
              {
                "type": "mrkdwn",
                "text": "Psssst this modal was designed using <https://api.slack.com/tools/block-kit-builder|*Block Kit Builder*>"
              }
            ]
          }
        ]
      }
    });

    console.log(result);
  }
  catch (error) {
    console.error(error);
  }
});
```
