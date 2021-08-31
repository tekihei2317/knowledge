# LocalStorageに保存するかSessionに保存するか

LocalStorageからSessionに保存するかを決める基準に保存する期間がある。Sessionには有効期限があるがLocalStorageには有効期限がないので、保存する期間が長い、もしくは分からない場合は、LocalStorageを使うと良さそう。あとLocalStorageには容量の制限がある。

## セキュリティについて少し

例えばCDNで読み込んでいるスクリプトに悪意があった場合、任意のJavaScriptを実行出来ることになる。つまり、攻撃者はLocalStorageやSession ID（クッキーに保存している場合）を盗むことが出来る。

TODO: XSS、CSRF

## LocalSorageの有効期限

有効期限はないらしい。HTML Living Standardを読んで下さい！（to 僕）

## Sessionの有効期限

クッキーに入っているSession IDは、その有効期限が切れれば消えてしまう。つまりそのSession IDに紐付いているデータが取得できなくなる。

サーバーに保存されているSession Dataにも有効期限があるかもしれない。php.iniで定義することが出来るみたいだったが、これがHTTPの仕様なのか、PHP以外の言語の場合はどうなのか、セッションをどこに保存していても消えるのか、などがよく分かっていない。

## メモ

- セッションIDはCookie以外にも保存することがある?
- LocalStorageはドメインごと?
- HTML Living Standardを読もう
  - [HTML Standard](https://html.spec.whatwg.org/multipage/webstorage.html#dom-localstorage)

## 参考
