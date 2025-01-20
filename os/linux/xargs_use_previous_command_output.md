# xargs use previous command output: 前のコマンドの出力を使用する

```sh
$ ls
file1  file2  file3

$ ls | xargs -i echo "arg is {}"
arg is file1
arg is file2
arg is file3
```
