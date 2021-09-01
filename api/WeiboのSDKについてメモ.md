# WeiboのAPIについて調査したメモ

## RubyのSDK

- [simsicon/weibo_2](https://github.com/simsicon/weibo_2)
  - [API - 微博API](https://open.weibo.com/wiki/API%E6%96%87%E6%A1%A3_V2)のラッパーらしい
  - omniauth、deviseと連携することも出来るみたい
- 認証はexampleがあるので、これを参考にする
  - [simsicon/weibo_2_example](https://github.com/simsicon/weibo_2_example)
  - リダイレクトURLが一致しないというエラーが出たけど、動きそうな感じはする

## メモ

- APIドキュメント
  - 中国語
    - [API - 微博API](https://open.weibo.com/wiki/API%E6%96%87%E6%A1%A3_V2)
  - 英語
    - [API文档 V2/en - 微博API](https://open.weibo.com/wiki/API%E6%96%87%E6%A1%A3_V2/en#Comments_API)
    - ~~[API文档/en - 微博API](https://open.weibo.com/wiki/API%E6%96%87%E6%A1%A3/en)~~
      - こっちはv1だった
  - 英語の方が詳しい気がする
    - favoriteとかtagsとかは英語の方にしか載ってなさそう
- [Messages api start - 微博API](https://open.weibo.com/wiki/Messages_api_start)
  - これは何? APIとはまた別の何か?
- 何をやるにしても、アクセストークンが必要そう

## 参考
