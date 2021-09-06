# WeiboのAPIの調査結果

## 調査結果まとめ

weiboの投稿、再投稿(リツイート)等のAPIが使えない可能性があります。アプリのレビューが通れば使えるようになる可能性があります。一部の投稿に関しては、別のAPIで代用出来る可能性があります。

## やりたいこと

現在使用しているTwitterの機能をWeiboの機能で置き換えること。Weibo APIを使って、Weiboに投稿をすること。

## やったこと

`statuses/update`（投稿を作成するAPI）にPOSTしました。そのときのエラーメッセージは以下です。

```text
Insufficient app permissions!: {"error":"Insufficient app permissions!","error_code":10014,"request":"/2/statuses/update.json"}
```

`statuses/update`は中国語のAPIドキュメント（2020年更新）には現在載っていません。英語版のドキュメント（2012年更新）には載っています。

中国語のAPIドキュメント: [API - 微博API](https://open.weibo.com/wiki/API%E6%96%87%E6%A1%A3_V2)
英語のAPIドキュメント: [API文档 V2/en - 微博API](https://open.weibo.com/wiki/API%E6%96%87%E6%A1%A3_V2/en#Write_API)

## 原因の調査

### 可能性1. OAuthのトークンのスコープが足りていない

管理画面に利用可能なAPIの一覧らしきもの（已有权限=許可を得る）がありましたが、そこに`statuses/update`はありませんでした。管理画面からスコープを追加するところはありましたが、`statuses/update`は存在しませんでした。

### 可能性2. アプリケーションのレビューが通らないと使用可能にならない

### 可能性3. APIエンドポイントがなくなっている

`statuses/update`が存在する英語のドキュメントの最終更新日が2012年なので、エンドポイント自体がなくなっている可能性があります。エラーメッセージで検索したところ、`statuses/update`の代わりに`statuses/share`を使ったという記事がいくつか見つかりました。

## 答え?

多分エンドポイント自体は残っている
理由: RubyのSDKのエンドポイントがそこになっている。よく使われていそうなPythonのSDKも多分そこを使っている。←READMEを見た感じ

多分権限が足りていない。申請する箇所が無かったのは、アプリケーションがレビューに通っていなかったため？レビューに通れば申請できるようになる気がする(要出典)

## 対応

### 1, 2の場合

アプリのレビューを通す（具体的に何をする？）通った後に、OAuthのトークンのスコープを広げる。

### 3の場合

`statuses/share`で代用出来るかを考える。`statuses/share`は、URLを含むweiboの投稿（URLのドメインは事前に管理画面で登録したものである必要がありそう）

## 参考

- `Insufficient App Permission`について
  - [机器交易009 微博失灵 | 易小阳交易志](http://yixiaoyang.com/jqjy009-wbsl/)
  - [Java新版本API发送新浪微博可能会出现的问题呢_Architect_CSDN的博客-CSDN博客](https://blog.csdn.net/Architect_CSDN/article/details/89383102)
  - [不能发表微博：weibo.APIError: APIError: 10014: Insufficient app permissions!, request: /2/statuses/update.json · Issue #59 · michaelliao/sinaweibopy](https://github.com/michaelliao/sinaweibopy/issues/59)
