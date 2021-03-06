Bolt アプリは `action` メソッドを用いて、ボタンのクリック、メニューの選択、メッセージショートカットなどのユーザーのアクションをリッスンすることができます。

アクションは文字列型の `action_id` または RegExp オブジェクトでフィルタリングできます。 `action_id` は、Slack プラットフォーム上のインタラクティブコンポーネントの一意の識別子として機能します。 

すべての `action()` の例で `ack()` が使用されていることに注目してください。Slack からイベントを受信したことを確認するために、アクションリスナー内で `ack()` 関数を呼び出す必要があります。これについては、「[イベントの確認](#acknowledge)」 セクションで説明しています。

*注: Bolt 2.x からメッセージショートカット（以前はメッセージアクションと呼ばれていました）は `action()` ではなく `shortcut()` メソッドを使用するようになりました。この変更については [2.x マイグレーションガイド](https://slack.dev/bolt/ja-jp/tutorial/migration-v2)を参照してください。*

```javascript
// action_id が "approve_button" のインタラクティブコンポーネントがトリガーされる毎にミドルウェアが呼び出される
app.action('approve_button', async ({ ack, say }) => {
  await ack();
  // アクションを反映してメッセージをアップデート
});
```
