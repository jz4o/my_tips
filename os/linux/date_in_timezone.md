# date in timezone: 特定のタイムゾーンの日時を取得する

```sh
$ date --date='@0'
# => Thu Jan  1 00:00:00 UTC 1970

$ TZ=Asia/Tokyo date --date='@0'
# => Thu Jan  1 09:00:00 JST 1970
```

* `date` の前に `TZ=<タイムゾーン>` を付与する

## 前提

* [Time Zone Database](https://ja.wikipedia.org/wiki/Tz_database) がインストールされていること

## 余談

* `date --date='@<エポック秒>'`
  * エポック秒を日付に変換する

