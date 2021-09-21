# fputcsvの問題点

空白が存在しない場合はダブルクォートで囲んでくれません。囲み文字の引数（$enclosure）もありますが、デフォルトでダブルクォートになっているため、これでは解決できなさそうです。

## 例

```php
<?php

$data = [
    "hoge",
    "ho ge",
    "ho hoge ",
    "ho　ge"
];

$stream = fopen("file.csv", "w");
fputcsv($stream, $data, ',', '"');
fclose($stream);
```

結果

```csv
hoge,"ho ge","ho hoge ",ho　ge
```

## 対処方法

自前で実装する。文字列にダブルクォートが含まれる場合はダブルクォートを重ねてエスケープすることに注意する。

```php
<?php

function putOneRowAsCSV($stream, $row, $lineBreak = "\n")
{
    $quotedRow = [];
    foreach ($row as $value) {
        // 文字列中のダブルクォートをエスケープする
        $escaped = str_replace('"', '""', $value);
        $quotedRow[] = "\"{$escaped}\"";
    }
    fwrite($stream, implode(',', $quotedRow) . $lineBreak);
}

$data = [
    "hoge",
    "ho ge",
    "ho hoge ",
    "ho　ge",
    "ho\"ge",
    '"a"b"c'
];

$stream = fopen("file.csv", "w");
putOneRowAsCSV($stream, $data);
fclose($stream);
```

結果

```text
"hoge","ho ge","ho hoge ","ho　ge","ho""ge","""a""b""c"
```

## 参考

- [【PHP】csvを自前で作った話 | ダブルコーテーション問題でfputcsvは使わず実装 - Qiita](https://qiita.com/non0311/items/b812aff80213f627d36b)
- [【PHP】CSV出力で値をダブルクォーテーションで囲う - suzu6の技術ブログ](https://www.suzu6.net/posts/207-php-csv-with-double-quotation/)

## メモ

`SplFileObject`を使うと良いみたいです。
