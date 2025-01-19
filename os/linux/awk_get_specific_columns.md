# awk get specific columns: 特定の列の値を取得する

```sh
$ ls -l
total 0
-rw-r--r-- 1 jz4o 197121 0 Jan 19 15:29 file1
-rw-r--r-- 1 jz4o 197121 0 Jan 19 15:29 file2
-rw-r--r-- 1 jz4o 197121 0 Jan 19 15:29 file3

$ ls -l | awk '{print $1, $3, $9}'
total
-rw-r--r-- jz4o file1
-rw-r--r-- jz4o file2
-rw-r--r-- jz4o file3
```
