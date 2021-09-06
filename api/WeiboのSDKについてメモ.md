# WeiboのAPIについて調査したメモ

## RubyのSDK

- [simsicon/weibo_2](https://github.com/simsicon/weibo_2)
  - [API - 微博API](https://open.weibo.com/wiki/API%E6%96%87%E6%A1%A3_V2)のラッパーらしい
  - omniauth、deviseと連携することも出来るみたい
- 認証はexampleがあるので、これを参考にする
  - [simsicon/weibo_2_example](https://github.com/simsicon/weibo_2_example)
  - リダイレクトURLが一致しないというエラーが出たけど、動きそうな感じはする

## メモ

- [Messages api start - 微博API](https://open.weibo.com/wiki/Messages_api_start)
  - これは何? APIとはまた別の何か?

## リンク

Weibo 開発者ページ

- [新浪微博开放平台-首页](https://open.weibo.com/index.php)

Weibo

- [微博-随时随地发现新鲜事](https://weibo.com/login.php)
- [微博日本站 - 随时随地发现新鲜事](https://jp.weibo.com/)

APIドキュメント

- [API - 微博API](https://open.weibo.com/wiki/API%E6%96%87%E6%A1%A3_V2)
- [API文档 V2/en - 微博API](https://open.weibo.com/wiki/API%E6%96%87%E6%A1%A3_V2/en#Comments_API)
  - 最終更新日2012年ですね...
  - 若干違うので(英語のほうがAPIが多い)、英語版にあるほうで使えないのがあるかもしれない
    - statuses/update.jsonは使えなさそうだった

APIのテストツール

- [API测试工具](https://open.weibo.com/tools/console)
  - 使いやすくはないのでトークンだけもらってPostmanでやると良さそう

## 参考

中国語

```text
1. 你好 / ニイ ハオ / こんにちは（一般的表現）
2. 您好 / ニン ハオ / こんにちは（丁寧語表現）
3. 吃饭了吗？ / チー ファン ラ マ / （親しい関係の）こんにちは。＜ご飯食べた？＞
4. 您好吗? / ニン ハオ マ / お元気ですか？
5. 身体好吗？ / シェン ティ ハオ マ / お元気ですか？
6. 早上好 / ザオ シャン ハオ / おはようございます。
7. 下午好 / シャー ウー ハオ / （午後の）こんにちは
8. 晩上好 / ワン シャン ハオ / こんばんは
9. 晩安 / ワン アン / おやすみなさい
10. 初次见面 / チュー ツー ジェン ミィエン / 初めまして
11. 我见到您很高兴 / ウォ ジェンダオ ニン ヘン ガオシン / お目にかかれてうれしいです
12. 好久不見 / ハオ ジュー ブ ジェン / お久しぶりです
13. 先走了 / シェン ズォ ラ / お先に
14. 辛苦了 / シン クー ラ / お疲れ様です
15. 再见 / ツァイ ジェン / さようなら
16. 明天见 / ミン ティエン ジェン / 又明日（会いましょう）
17. 拜拜 / バイ バイ / さようなら
18. 忙吗？ / マン マ / お忙しいですか？
19. 请进 / チン ジン / どうぞお入り下さい
20. 不客气 / ブー カー チー / お気遣い無く
```
