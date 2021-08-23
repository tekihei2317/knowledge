# Laravelのセッションの基礎

## セッションとは何か

- クライアントにIDを保存し、それに対応するデータをサーバー側に保存すること
  - クライアント側のIDをセッションIDといい、Cookieなどに保存する
  - サーバー側のデータはファイルやRedisに保存する

## Laravelのセッション

- sessionにfalseを入れるとnullになるみたい
- ファイルに保存している場合の確認方法を知りたい
  - データ以外にも情報が書かれているっぽい
- bladeからのアクセス方法
  - sessionメソッドで取得できる
  - これはPHPのメソッド？Laravelのメソッド？

## 参考

- [HTTP Session - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/8.x/session#introduction)
