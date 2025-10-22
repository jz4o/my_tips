# 任意のサイズのランダムなデータファイルを作成する

```powershell
function New-RandomDataFile($FilePath, $FileSize) {
  $bytes = [byte[]]::new($FileSize)
  (New-Object System.Security.Cryptography.RNGCryptoServiceProvider).GetBytes($bytes)
  [System.IO.File]::WriteAllBytes($FilePath, $bytes)
}
```

## 引数

* `$FilePath`
  * 出力するファイルパス
* `$FileSize`
  * 出力するファイルのサイズ

## 例

```powershell
New-RandomDataFile dummy_file 10MB
```
