# LaravelでIPアドレスを取得する

`$request->ip()`で取得出来るが。しかし、リバースプロキシを使っている場合は、リバースプロキシのIPアドレスが取得されるらしい。

リバースプロキシの場合でも取得するには、HTTPの`HTTP_X_FORWARDED_FOR`ヘッダから取得する方法と、Requestクラスにオプションを設定する方法がある。

## 参考

- [LaravelでIPアドレスを取得する](https://leben.mobi/blog/laravel_ip_address/php/)
- [Request::ip()でIPアドレスの取得 - Qiita](https://qiita.com/kawax/items/044d5a1846232938303f)
