# gcd: 2つの数値の最大公約数を計算する

```ts
const gcd: (a: number, b: number) => number = (a: number, b: number): number => {
    const min: number = Math.min(a, b);
    const max: number = Math.max(a, b);

    return min === 0 ? max : gcd(min, max % min);
};
```

## 引数

* `a`
  * 数値
* `b`
  * 数値

## 例

```ts
gcd(18, 24);
// => 6

gcd(649, 826);
// => 59

gcd(7, 100);
// => 1
```
