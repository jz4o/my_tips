# converting images to black and white: 画像を白黒加工する

* 黒加工

  ```css
  img, svg {
    filter: brightness(0);
    /* 明るさを0%（黒）にする */
  }
  ```

* 白加工

  ```css
  img, svg {
    filter: brightness(0) invert(1);
    /* 明るさを0%（黒）にしたのち、色を100%反転（黒 -> 白）する */
  }
  ```

## 前提

* 画像が透過処理されていること

## 補足

* 関数は宣言順に実行されるため、順序を変更すると表示も変わる

## 参考

* [filter](https://developer.mozilla.org/ja/docs/Web/CSS/filter)
* [brightness()](https://developer.mozilla.org/ja/docs/Web/CSS/filter-function/brightness)
* [invert()](https://developer.mozilla.org/ja/docs/Web/CSS/filter-function/invert)
