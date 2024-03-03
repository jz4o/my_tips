# dynamic matrix: 動的に matrix を設定する

```yaml
name: dynamic-matrix
on:
  workflow_dispatch:
    inputs:
      matrix-size:
        type: number
        default: '1'
        required: true

jobs:
  set-matrix-value:
    runs-on: ubuntu-latest
    outputs:
      matrix-value: ${{ steps.set-matrix-value.outputs.matrix }}

    steps:
      - name: set matrix value
        id: set-matrix-value
        run: |
          echo "matrix=[$(seq -s ',' 1 ${{ inputs.matrix-size }})]" >> $GITHUB_OUTPUT

  run-matrix:
    runs-on: ubuntu-latest
    needs: set-matrix-value
    strategy:
      matrix:
        value: ${{ fromJson(needs.set-matrix-value.outputs.matrix-value) }}

    steps:
      - name: echo matrix value
        run: |
          echo ${{ matrix.value }}
```

## matrix の値設定箇所

```yaml
set-matrix-value:
  outputs:
    matrix-value: ${{ steps.set-matrix-value.outputs.matrix }}

  steps:
    - name: set matrix value
      id: set-matrix-value
      run: |
        echo "matrix=[$(seq -s ',' 1 ${{ inputs.matrix-size }})]" >> $GITHUB_OUTPUT
```

* NAME=[VALUE1, VALUE2, ...] の形で `$GITHUB_OUTPUT` に書き込む
* `$GITHUB_OUTPUT` に書き込んだ値を job の outputs に書き込む

## matrix 設定箇所

```yaml
run-matrix:
  needs: set-matrix-value
  strategy:
    matrix:
      value: ${{ fromJson(needs.set-matrix-value.outputs.matrix-value) }}
```

* needs を指定し、 matrix の値設定後に job を実行する
* matrix の値を配列として指定する

