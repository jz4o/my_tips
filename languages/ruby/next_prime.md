# next_prime: 指定された値の次の素数を取得する

```rb
require 'prime'

def next_prime(n)
  return 2 if n < 2

  temp_n = n.to_i
  temp_n = temp_n.even? ? temp_n.next : temp_n + 2
  temp_n += 2 until temp_n.prime?

  temp_n
end
```

## 引数

* `n`
  * 数値
 
## 戻り値

* 受け取った値の次の素数

## 例

```rb
next_prime -1
# => 2

next_prime 2
# => 3

next_prime 23.4
# => 29

next_prime 89
# => 97
```
