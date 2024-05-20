# each_slice: リストを要素数 n に分割する

```py
def each_slice(target_list: list, n: int):
    return [target_list[i:i + n] for i in range(0, len(target_list), n)]
```

## 引数

* `target_list`
  * 分割対象のリスト
* `n`
  * 分割後のリストの要素数

## 例

```py
each_slice([1, 2, 3, 4, 5], 2)
# => [[1, 2], [3, 4], 5]]

each_slice(['a', 'b', 'c', 'd', 'e'], 3);
# => [['a', 'b', 'c'], ['d', 'e']]

each_slice(['a', 'b', 'c', 'd', 'e'], 10);
# => [['a', 'b', 'c', 'd', 'e']]
```
