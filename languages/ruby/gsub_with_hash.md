# gsub with hash: Hashを使用して文字列を置換する

```rb
def gsub_with_hash(text, replace_hash)
  transform_hash = replace_hash.transform_keys(&:to_s)
  text.gsub Regexp.union(transform_hash.keys), transform_hash
end
```

## 引数

* `text`
  * 置き換える対象の文字列
* `replace_hash`
  * 置き換えるパターン

## 戻り値

* 置換後の文字列

## 例

```rb
hash = {
  one: '1',
  two: '2',
  three: '3'
}

replaced = gsub_with_hash 'one two three four five', hash
puts replaced
# => 1 2 3 four five
```

## 参考

* [Regexp.union](https://docs.ruby-lang.org/ja/latest/class/Regexp.html#S_UNION)
