# dynamic variable: 動的に環境変数を設定する

```yaml
name: dynamic-variable
on:
  workflow_dispatch

jobs:
  test-dynamic-variable:
    runs-on: ubuntu-latest

    steps:
      - name: set env
        run: |
          echo "TEST=OK" >> $GITHUB_ENV

      - name: get env
        run: |
          echo ${{ env.TEST }}
          # => OK
```

## 環境変数設定箇所

```yaml
- name: set env
  run: |
    echo "TEST=OK" >> $GITHUB_ENV
```

* NAME=VALUE の形で `$GITHUB_ENV` に書き込む

## 環境変数参照箇所

```yaml
- name: get env
  run: |
    echo ${{ env.TEST }}
```

* env.NAME の形で参照する

## 参考

* [GitHub Actions のワークフロー コマンド#環境変数の設定](https://docs.github.com/ja/actions/using-workflows/workflow-commands-for-github-actions#setting-an-environment-variable)

