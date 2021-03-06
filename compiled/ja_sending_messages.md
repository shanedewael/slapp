リスナー関数内では、その実行に関連付けられた会話 (例：リスナー実行のトリガーが発生したイベント・アクションが発生したチャンネル) があるとき `say()` を使用できます。 `say()` は、シンプルなメッセージを送信するための文字列か、もっと複雑なメッセージを送信するための JSON ペイロードを受け付けます。渡されたメッセージのペイロードは、関連付けられた会話へ送信されます。

リスナー関数以外の場所でメッセージを送信したい場合や、より高度な操作 (特定のエラーの処理など) を実行したい場合は、[Bolt インスタンスにアタッチされた client を使用](#web-api)して `chat.postMessage` を呼び出します。

```javascript
// "knock knock" を含むメッセージをリッスンし、 "who's there?" というメッセージをイタリック体で送信
app.message('knock knock', async ({ message, say }) => {
  await say(`_Who's there?_`);
});
```
