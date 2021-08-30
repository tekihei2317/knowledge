# Carbonで日付をフォーマットする

現在日時を取得してファイル名に付けたかったため。

## 実装

```php
Carbon::now()->format('YmdHis');
// "20210827030113"

Carbon::now()->toDateTimeString();
// "2021-08-27 03:03:36"
```

Carbonを使うのが良さそう。Carbonのformatメソッドを使う。Carbonのformatメソッドは、PHPのDateTime::format()と同じ形式が使えるみたい。こういう日付の形式はどの言語でも共通する定義みたいなのがあるのでしょうか。

ドキュメントから推測するに、年、月、日付、時間、分、秒はそれぞれYmdHisを使えば良さそうだった。

ファイル名に空白が入っていいのであればtoDateTimeStringを使えばよさそう。拡張子のついているファイルに空白があると違和感があったので、空白は空けないことにした。

## 参考

- [Carbon - A simple PHP API extension for DateTime.](https://carbon.nesbot.com/docs/#api-formatting)
