# lcm: 2つの数値の最小公倍数を計算する

```ts
const lcm: (a: number, b: number) => number = (a: number, b: number): number => {
    return a / gcd(a, b) * b;
};
```

## 引数

* `a`
  * 数値
* `b`
  * 数値

## 例

```ts
lcm(12, 18);
// => 36

lcm(100, 101);
// => 10100

lcm(0, 100);
// => 0
```

## 参考

* [gcd: 2つの数値の最大公約数を計算する](./gcd.md)
