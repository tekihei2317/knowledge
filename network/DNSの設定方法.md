# DNSの設定方法

## 基礎用語

- Aレコード
  - ドメインとIPアドレスの対応を表す
- CNAMEレコード
  - ドメインに別名をつける
- ドメインの浸透
  - [DNS Checker - DNS Propagation Check & DNS Lookup](https://www.whatsmydns.net/#CNAME/blog.tekihei2317.com)で確認できる
  - 浸透するとnslookupで確認できるようになる

## 疑問点

- サブドメインを、普通のドメインと別のIPアドレスに割り振れる？
  - 別々のAレコードを定義すれば良さそう
    - `blog.example.com → x.x.x.x`
    - `example.com → y.y.y.y`
  - 同じIPアドレスを割り当てることも出来る?
    - CNAMEでやるのが普通だと思うけど
- CNAMEで別のdnsサーバーをしているやつ
  - お名前ドットコムでvercelのDNSサーバーを指定した
  - 直接IPアドレスを指定してもいいのかな

## 参考

- [なぜ「DNSの浸透」は問題視されるのか (4):Geekなぺーじ](https://www.geekpage.jp/blog/?id=2011-10-27/1&p=4)
  - キャッシュの仕組みを理解することが重要っぽい
