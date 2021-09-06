# Weibo投稿を実装する

## とりあえずアクセストークンの有効期限を見る

### アクセストークンの有効期限は？

レスポンスを見ると5年になっていた。`expires_in`が約`5*365*24*60*60`秒で、`expires_at`が5年後のUNIXタイムスタンプだった。

### エンドポイントは正しいか?

ライブラリにbinding.irbで仕込んで確認すると、`https://api.weibo.com/oauth2/access_token`になっていたので合っていそう。tcpdumpで見たほうが確実な気はする。

### 5年という期間は何で決まっているか？

### 5年という期間は変更することが出来るか？

[授权机制说明 - 微博API](https://open.weibo.com/wiki/%E6%8E%88%E6%9D%83%E6%9C%BA%E5%88%B6#.E6.8E.88.E6.9D.83.E6.9C.89.E6.95.88.E6.9C.9F)に書いてありそうな気がする。
アクセストークンの有効期限は、アプリがテスト状態のときは1日、テストが通れば30日と書いてあるっぽい。

## スコープが足りなくてエラーになる

```text
Insufficient app permissions!: {"error":"Insufficient app permissions!","error_code":10014,"request":"/2/statuses/update.json"}
```

管理画面から、アプリの権限を追加する必要がある？もしかしてアプリの監査に通らなければ投稿できない？

投稿作成（再投稿）でも同じエラーになった。

### 解決方法を調べる

アプリの認証が通れば使えるようになる可能性はある。

アプリの管理画面で設定できる場所がある？
見た感じはなさそうだった。

### APIが変わっているのかもしれない

英語版のドキュメントには`statuses/update.json`があったが、中国語版には無かった
→アップデートで使えなくなった?

英語のドキュメントの最終更新日が2012年だったので全然ありうる。中国語は2020年だった。

`statuses/update`の代わりに`statuses/share`を使ったという記事がいくつか見つかる。

- [机器交易009 微博失灵 | 易小阳交易志](http://yixiaoyang.com/jqjy009-wbsl/)
- [Java新版本API发送新浪微博可能会出现的问题呢_Architect_CSDN的博客-CSDN博客](https://blog.csdn.net/Architect_CSDN/article/details/89383102)
- [不能发表微博：weibo.APIError: APIError: 10014: Insufficient app permissions!, request: /2/statuses/update.json · Issue #59 · michaelliao/sinaweibopy](https://github.com/michaelliao/sinaweibopy/issues/59)

### メモ

可能性を考える

#### APIエンドポイントが使用不可能になっている

エラーが返ってくるのでそれはない気がするけど、他の人は別のエンドポイントを使っているのでそうかもしれない。

#### 書き込みのエンドポイントを使うためには、追加の操作をする必要がある

状況から考えると、この可能性が高いと思う。追加の操作は管理画面から申請するか、アプリの申請をするか。管理画面から操作できそうな項目はなさそうだった。申請に通る必要がある気がする。

とりあえず分からないのでドキュメントを読みます。

[ビギナーズガイド-WeiboAPI](https://open.weibo.com/wiki/%E6%96%B0%E6%89%8B%E6%8C%87%E5%8D%97)
「信用実績のある開発者は、高度な書き込みインターフェイスに申し込むことが出来る」とあります。申し込むと投稿が出来るようになるかもしれない。2014年の情報なので古いかもしれない。
