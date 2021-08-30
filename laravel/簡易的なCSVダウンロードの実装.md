# 簡易的なCSVダウンロードの実装

ファイルをダウンロードするHTTPレスポンスを、ブラウザに返却してあげれば良い。

## 実装

### ファイルとして保存しない場合

`streamDownload`を使う。`streamDownload`は、標準出力に出力したものをファイルとしてダウンロードさせるみたい。

```php
// コントローラー
return response()->streamDownload(function () {
    Post::outputCsv();
}, $fileName);

// モデル
public static function outputCsv()
{
    $header = ['ID', 'タイトル' '内容'];
    $rows = [
        1, 'タイトル1', 'テスト投稿',
        2, 'タイトル2', 'テスト投稿',
    ];
    Csv::writeToOutputStream($header, $rows);
}

// CSV出力クラス
public static function writeToOutputStream(array $header, array $rows)
{
    $stream = fopen('php://output', 'w');

    fputcsv($stream, $header);
    foreach ($rows as $row) {
        fputcsv($stream, $row);

    }
    fclose($stream);
}
```

### ファイルとして保存している場合

TODO:

## 参考

- [HTTPレスポンス 8.x Laravel](https://readouble.com/laravel/8.x/ja/responses.html)
- [LaravelでCSVダウンロード。 - Qiita](https://qiita.com/niiyz/items/83770cfa6d6bb33c10ab)
