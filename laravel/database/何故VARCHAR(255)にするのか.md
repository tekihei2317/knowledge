# 何故VARCHAR(255)にするのか

## 理由

- utf8の場合、uniqueインデックスを追加できる最大のサイズのため
  - VARCHAR(255)だとuniqueインデックスを追加できるが、VARCHAR(256)だと追加できない
- 767バイトの制限があるらしい
  - utf8の場合: 767 / 3 = 255文字
  - utf8mb4の場合 767 / 4 = 191文字

## 疑問点

- utf8ってどういう文字であっても1文字あたり3バイト?
- VARCHAR(255)の255は文字数を表す?

## 参考

- [MySQLにおけるvarchar(255)とvarchar(256)の違い | なまけものノこえだめ](https://www.namakedame.work/mysql-varchar-255-256/)
- [DB設計のときによく使いそうな最大長(maximum length)まとめ - 君たちは永遠にそいつらより若い](https://kuteken.hatenablog.com/entry/2015/02/24/201015)
  - 電話番号は16文字で良さそう
  - メールアドレスは255文字のままで良さそう
