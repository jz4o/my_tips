# get variable from selected of inputs: inputs で選択された値から変数を取得する

```yaml
name: get-variable-from-selected-of-inputs

on:
  workflow_dispatch:
    inputs:
      variable-name:
        description: "variable name"
        required: true
        type: choice
        options:
          - blue
          - green

jobs:
  get-variable-from-selected-of-inputs:
    runs-on: ubuntu-latest
    steps:
      - name: get variable
        run: |
          echo ${{ vars[inputs.variable-name] }}
```

## Prefixを付与して変数を取得する例

```yaml
name: get-variable-by-prefixing-selected-input

on:
  workflow_dispatch:
    inputs:
      variable-name:
        description: "variable name"
        required: true
        type: choice
        options:
          - blue
          - green

jobs:
  get-variable-by-prefixing-selected-input:
    runs-on: ubuntu-latest
    steps:
      - name: get variable
        run: |
          echo ${{ vars[format('PREFIX_{0}', inputs.variable-name)] }}
```

## 参考

* [Evaluate expressions in workflows and actions](https://docs.github.com/ja/actions/writing-workflows/choosing-what-your-workflow-does/evaluate-expressions-in-workflows-and-actions#format)
