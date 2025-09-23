# 定期実行関数

```js
class PeriodicFunction {
  // 実行間隔（ミリ秒）
  static interval = 1000;

  // 処理本体
  static exec = () => {
    // 定期実行する処理
  };

  // 定期実行開始処理
  static start = () => {
    if (this.intervalId) {
      return;
    }

    this.intervalId = setInterval(this.exec, this.interval);
  };

  // 定期実行終了処理
  static stop = () => {
    if (!this.intervalId) {
      return;
    }

    clearInterval(this.intervalId);
    delete this.intervalId;
  };
}
```

## 使用例

### 画面表示時に定期実行を開始し、画面が非表示の時は実行を停止する

```js
window.addEventListener('load', () => {
  document.addEventListener('visibilitychange', () => {
    if (document.visibilityState === 'visible') {
      // タブが表示状態になったときに即時実行し、定期実行も開始
      PeriodicFunction.exec();
      PeriodicFunction.start();
    } else {
      // タブが非表示になったときに定期実行を停止
      PeriodicFunction.stop();
    }
  });

  // 定期実行開始
  PeriodicFunction.start();
});
```

## 参考

* [Window: setInterval() メソッド](https://developer.mozilla.org/ja/docs/Web/API/Window/setInterval)
* [Window: clearInterval() メソッド](https://developer.mozilla.org/ja/docs/Web/API/Window/clearInterval)
