# タブの表示状態が変更された時に処理を行う

```js
document.addEventListener('visibilitychange', () => {
  if (document.visibilityState === 'visible') {
    // タブが表示状態になったときの処理
  } else {
    // タブが非表示になったときの処理
  }
});
```

## 参考

* [Document: visibilitychange イベント](https://developer.mozilla.org/ja/docs/Web/API/Document/visibilitychange_event)
* [Document: visibilityState プロパティ](https://developer.mozilla.org/ja/docs/Web/API/Document/visibilityState)
