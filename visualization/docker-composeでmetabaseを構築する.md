# docker-composeでmetabaseを構築する

MySQLの文字コードとか認証方式とかいつもつまづいて調べているのでまとめたい。


## 発生したエラー

```text
java.sql.SQLTransientConnectionException: Could not connect to address=(host=mysql)(port=3306)(type=master) : RSA public key is not available client side (option serverRsaPublicKeyFile not set)
```

MySQL8で認証方式が`caching_sha2_password`になっていることが原因らしい。以下を参考にしてMySQLの接続文字列に`allowPublicKeyRetrieval=true`をつけると繋がった。

[Migrating from H2 to MySQL: RSA public key is not available client side (option serverRsaPublicKeyFile not set) · Issue #12545 · metabase/metabase](https://github.com/metabase/metabase/issues/12545)
