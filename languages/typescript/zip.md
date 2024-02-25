# zip: 2つの配列の各要素からなる配列の配列を生成する

```ts
const zip: <T, U>(a: T[], b: U[]) => [T, U][] = <T, U>(a: T[], b: U[]): [T, U][] => {
    const arraySize: number = Math.max(a.length, b.length);
    return [...Array(arraySize).keys()].map(index => {
        return [a[index], b[index]];
    });
};
```

## 引数

* `a`
  * 配列
* `b`
  * 配列

## 例

```ts
zip(['a', 'b', 'c'], [1, 2, 3]);
// => [['a', 1], ['b', 2], ['c', 3]]

zip(['a', 'b'], [1, 2, 3]);
// => [['a', 1], ['b', 2], [undefined, 3]]

zip([['a', 'b'], ['c', 'd'], ['e', 'f']], [1, 2, 3]);
// => [[['a', 'b'], 1], [['c', 'd'], 2], [['e', 'f'], 3]]
```

