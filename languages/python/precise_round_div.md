# precise_round_div: 精密な除算を行う

```py
from __future__ import annotations

from decimal import Decimal, ROUND_HALF_UP

def precise_round_div(dividend: float, divisor: float, ndigits: int | None = None) -> float:
    div_decimal = Decimal(str(dividend)) / Decimal(str(divisor))

    if ndigits is None:
        return float(div_decimal)
    
    adjust_decimal = Decimal(str(10 ** -ndigits))
    rounded_decimal = (div_decimal / adjust_decimal).quantize(Decimal('0'), ROUND_HALF_UP) * adjust_decimal

    return float(rounded_decimal)
```

## 引数

* `dividend`
  * 被除数
* `divisor`
  * 除数
* `ndigits`
  * 丸める位
    * 指定しない場合、丸め処理をしない
    * 0の場合、小数点以下を四捨五入する
    * 0より大きい場合、小数点以下の指定された位で四捨五入する
    * 0より小さい場合、小数点以上の指定された位で四捨五入する

## 戻り値

* 計算結果の float

## 例

```py
43362 / 86.4
# => 501.87499999999994

precise_round_div(43362, 86.4)
# => 501.875

precise_round_div(43362, 86.4, 2)
# => 501.88

precise_round_div(43362, 86.4, 0)
# => 502.0

precise_round_div(43362, 86.4, -1)
# => 500.0

precise_round_div(43362, 86.4, -3)
# => 1000.0

precise_round_div(43362, 86.4, -4)
# => 0.0
```

## 補足

* Decimal オブジェクトの生成には文字列を渡すのが安全
  ```py
  Decimal(86.4)
  # => 86.400000000000005684341886080801486968994140625

  Decimal('86.4')
  # => 86.4
  ```

## 参考

* [module-decimal](https://docs.python.org/ja/3/library/decimal.html#module-decimal)
* [decimal.Decimal.quantize](https://docs.python.org/ja/3/library/decimal.html#decimal.Decimal.quantize)
