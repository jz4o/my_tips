# prime_division: 整数を素因数分解する

```py
import math

def prime_division(n):
    prime_counts = []

    temp_n = n
    for prime in range(2, math.isqrt(temp_n) + 1):
        if temp_n % prime != 0:
            continue

        count = 0
        while temp_n % prime == 0:
            temp_n //= prime
            count += 1

        prime_counts.append((prime, count))

    if temp_n >= 2:
        prime_counts.append((temp_n, 1))

    return prime_counts
```

## 引数

* `n`
  * 素因数分解する任意の整数
 
## 戻り値

* 素因数とその指数からなる tuple の list

## 例

```py
prime_division(10)
# => [(2, 1), (5, 1)]

prime_division(12)
# => [(2, 2), (3, 1)]

prime_division(1)
# => []
```
