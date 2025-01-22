# tail get after specific row number: 指定の行番号以降を取得する

```sh
$ pip list
Package    Version
---------- -------
pip        24.3.1
setuptools 75.8.0

$  pip list | tail -n +3
pip        24.3.1
setuptools 75.8.0
```

## 余談

* `+` をつけないと末尾から指定の行数を取得する
  ```sh
  $ pip list | tail -n 3
  ---------- -------
  pip        24.3.1
  setuptools 75.8.0
  ```
