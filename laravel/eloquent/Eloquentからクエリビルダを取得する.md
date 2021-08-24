# Eloquentからクエリビルダを取得する

メソッドを直接呼ぶか、queryメソッドを呼べば良い。

```php
Post::query()->max('id');
Post::max('id');
```

- アソシエーションを呼んでもEloquentビルダーが返ってくる
- メソッドを直接呼ぶと、Eloquentビルダーが返ってくるような気がする
  - 処理を委譲しているのかな

```php
Post::with('user');
```

- ポイント
  - モデルクラスにstaticメソッドが存在しない場合は`Illuminate\Database\Eloquent\Builder`（Eloquentビルダー）に委譲される
  - Eloquentビルダーにメソッドが存在しない場合は`Illuminate\Database\Query\Builder`（Queryビルダー）に委譲される
- EloquentビルダーはQueryビルダーのラッパークラス

## クエリを観察する方法

- クエリビルダの場合
  - `toSql()`と`getBindings()`を使う
- クエリビルダ以外の場合
  - `\DB::enableQueryLog()`の後に、`\DB::getQueryLog()`を使う
  - tinkerでクエリログを空にする方法は分からなかった

## 参考

- [【Laravel5】Eloquent ORMと2つのBuilderクラス｜Laravel｜PHP｜開発ブログ｜株式会社Nextat（ネクスタット）](https://nextat.co.jp/staff/archives/131)
- [Laravel SQLの実行クエリログを出力する - Qiita](https://qiita.com/ucan-lab/items/753cb9d3e4ceeb245341)  
