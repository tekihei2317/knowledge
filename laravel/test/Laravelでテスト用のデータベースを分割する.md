# Laravelでテスト用のデータベースを作成する

`php artisan test --env=testing`と実行すると、`.env.testing`を読み込んでくれるみたいなので、`.env.testing`で接続先を切り替える方法でやってみました。

リポジトリはこちら: TODO:

## 手順

1. テスト用のデータベースの作成
2. `.env.testing`の作成
3. テストの作成・実行

## テスト用のデータベースの作成

Dockerを使用していたため、初期化スクリプトでデータベースを作成しました。データベース名は、後ろにtestingとつけるのが慣習（？）のようです。`<DBの名前>`などは適切な値で置き換えます。

```sql
-- docker/mysql/entrypoint/initialize.sql
create database <DBの名前>;
grant all privileges on <DBの名前>.* to <ユーザー名>@'%';
```

これを入れたディレクトリを、docker-compose.ymlで`/docker-entrypoint-initdb.d`にマウントしました（Dockerfileを使っている場合はCOPYしたほうがいいかもしれません）。

コンテナを作り直して設定を反映します。これでテスト用のデータベースを作成することが出来ました。

```bash
docker-compose down && docker-compose up -d
```

## .env.testingの作成

現在使用している.envを.env.testingにコピーして、`DB_DATABASE`の値を先程作成したデータベースの名前に変更します。

```bash
cp .env .env.testing
sed -i -e 's/DB_DATABASE=.*/DB_DATABASE=<DBの名前>/' .env.testing
```

## テストの作成、実行

DBとの接続を確認するためのテストを作成します。

```bash
php artisan make:test SampleTest
```

作成したテストに以下を追加します。

```php
// tests/Feature/SampleTest.php
$this->assertEquals(User::count(), 0);
```

テストを実行します。

```bash
php artisan test --env=testing tests/Feature/SampleTest.php
```

テストが通れば無事にDBと接続出来ています。初回のテストを実行した際にマイグレーションが実行されるので、マイグレーションの実行は不要なようです。

## 参考

- [laravelでDBテストコードを書く前の設定すべきこと - Qiita](https://qiita.com/kuriya/items/4c9dbefc19514f415374)
- [【Docker】MySQLで複数database環境を構築する - Qiita](https://qiita.com/piggydev/items/2096258dc45a6bbe2a19)
- [Laravel × Docker でテスト用のデータベースコンテナを使う - Qiita](https://qiita.com/ucan-lab/items/0f7100f08a062e892c52)
