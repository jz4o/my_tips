# 大域脱出

```py
for i in range(3):
    for j in range(10):
        value = i * 10 + j
        if value == 13:
            break

        print(value)

    else:
        # 直前の for が正常終了すると else に入る
        continue

    # 直前の for が break で終了されると else を通らずにここに来る
    break

# =>
# 0
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
# 10
# 11
# 12
```

## 参考

* [ループの else 節](https://docs.python.org/ja/3/tutorial/controlflow.html#else-clauses-on-loops)
