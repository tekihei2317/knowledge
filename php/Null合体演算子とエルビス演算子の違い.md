# Null合体演算子とエルビス演算子の違い

Null合体演算子（??）は`isset($a) ? $a : $b`の省略形で、エルビス演算子は`$a ? $a : $b`の省略形。

`isset($x)`は、`$x`が定義されていてかつ`null`でないときに`true`になり、`(bool)$x`は、以下の値のときに`false`になる。

| Falsyな値 |
| --------- |
| ""        |
| null      |
| false     |
| 0         |
| '0'       |
| []        |
| 未定義(warningが出る)          |

```php
// REPLで試した結果
>>> array_map(fn($x) => (bool)$x, ["", null, false, 0, '0', [], $var]);
// <warning>PHP Notice:  Undefined variable: var in /Users/gib0017/.anyenv/envs/phpenv/versions/7.4.9eval()'d code on line 1</warning>
=> [ false, false, false, false, false, false, false ]

>>> array_map(fn($x) => (bool)$x, [1, 42, -1, "1", "-1", "true", "false"]);
=> [ true, true, true, true, true, true, true ]
```

## 参考

- [PHP: PHP 型の比較表 - Manual](https://www.php.net/manual/ja/types.comparisons.php)
- [PHPの真偽・空判定まとめ｜開発室ブログ｜株式会社アクセスジャパン](https://access-jp.co.jp/blogs/development/42)
- [似てるようで違う、PHPのエルビス演算子とNull合体演算子 - Qiita](https://qiita.com/jay-es/items/3b8734bc02070d074a3e)
