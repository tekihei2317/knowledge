# Weibo認証を実装する

## メモ

- サードパーティーアプリの認証前は、アプリケーションを登録したユーザーでしかWeiboログインできないみたい
  - [Imitate the appearance of Sina Weibo project {"error": "applications over the unaudited use restrictions!", "Error_code": 21321, "request"(Others-Community)](https://titanwolf.org/Network/Articles/Article?AID=30af2a42-83a0-4c0e-a588-38f2492f48eb#gsc.tab=0)
  - [新浪微博授权失败：applications over the unaudited use restrictions - LittleEyes - 博客园](https://www.cnblogs.com/ryq2014/p/5280344.html)

## Weiboではアプリのテスト期間中は、アプリを登録したユーザーでしか認証ができない

### 状況

Weiboログイン（Fansの認可）をしようとすると、以下のエラーが発生します。

```text
OAuth2::Error at /callback
applications over the unaudited use restrictions!: {"error":"applications over the unaudited use restrictions!","error_code":21321,"request":"/2/users/show.json"}`
```

### 原因

未レビューのアプリケーションには制限がかかっているため。アプリのレビュー前は、アプリを登録したユーザーでしか、アプリの認可をすることが出来ないようです。

参考

- [Imitate the appearance of Sina Weibo project {"error": "applications over the unaudited use restrictions!", "Error_code": 21321, "request"(Others-Community)](https://titanwolf.org/Network/Articles/Article?AID=30af2a42-83a0-4c0e-a588-38f2492f48eb#gsc.tab=0)
- [Error code - 微博API](https://open.weibo.com/wiki/Error_code)
  - 未审核的应用使用人数超过限制（ユーザー数が制限値を超える未監査のアプリケーション）の場合、このエラーが発生するとあります。
