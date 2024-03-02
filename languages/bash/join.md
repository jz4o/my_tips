# join: 配列を文字列連結する

```sh
join() {
    declare -n target_array=$1
    sep="${2:- }"

    IFS="$sep"
    echo "${target_array[*]}"
}
```

## 引数

* `$1`
  * 配列の変数名
* `$2` (省略可)
  * 区切り文字列
  * 省略した場合は半角スペース

## 例

```sh
array=(1 2 3)
joined_array=$(join 'array' ',')
echo "$joined_array"
# => 1,2,3

array=(1 2 3)
joined_array=$(join 'array')
echo "$joined_array"
# => 1 2 3

array=('test 1' 'test 2' 'test 3')
joined_array=$(join 'array' ',')
echo "$joined_array"
# => test 1,test 2,test 3
```

## 補足

* 関数に渡す配列の変数名と関数内の配列の変数名が被っていると動作しない

  ```sh
  target_array=(1 2 3)
  joined_array=$(join 'target_array' ',')
  # => declare: warning: target_array: circular name reference
  ```

