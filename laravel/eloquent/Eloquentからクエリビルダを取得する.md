# Eloquentからクエリビルダを取得する

メソッドを直接呼ぶか、queryメソッドを呼べば良い。

```php
Post::query()->max('id');
Post::max('id');
```
- ポイント
  - モデルクラスにstaticメソッドが存在しない場合は`Illuminate\Database\Eloquent\Builder`（Eloquentビルダー）に委譲される
  - Eloquentビルダーにメソッドが存在しない場合は`Illuminate\Database\Query\Builder`（Queryビルダー）に委譲される
- EloquentビルダーはQueryビルダーのラッパークラス


## 参考
- [【Laravel5】Eloquent ORMと2つのBuilderクラス｜Laravel｜PHP｜開発ブログ｜株式会社Nextat（ネクスタット）](https://nextat.co.jp/staff/archives/131)
