# join: 配列を文字列連結する

```sh
sed "s/ /<区切り文字列>/g" <<< "<配列>"
```

## 例

```sh
array=(1 2 3)
sep=','
joined_array=$(sed "s/ /${sep}/g" <<< "${array[@]}")

echo "$joined_array"
# => 1,2,3
```

