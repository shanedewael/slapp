---
title: Listening to messages
slug: message-listening
order: 1
---

<div class="section-content">
To listen to messages that [your app has access to receive](https://api.slack.com/messaging/retrieving#permissions), you can use the `message()` method. This method adds listener middleware that filters out any events that aren’t of type `message`.

It accepts an optional `pattern` parameter of type `string` or `RegExp` object that will filter out any messages that don’t match.
</div>

```javascript
// This will match any message that contains 👋
app.message(':wave:', async ({ message, say}) => {
  say(`Hello, <@${message.user}>`);
});
```

<details markdown="0">
<summary class="section-head">
<h4 class="section-head">Using a RegExp pattern</h4>
</summary>

<div class="secondary-wrapper">

<div class="secondary-content">
A RegExp pattern can be used instead of a string for more granular matching.

All of the results of the RegExp match will be in `context.matches`.
</div>

```javascript
app.message(/^(hi|hello|hey).*/, async ({ context, say }) => {
  // RegExp matches are inside of context.matches
  const greeting = context.matches[0];
  
  say(`${greeting}, how are you?`);
});
```

</div>
</details>