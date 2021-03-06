# Laravelでクエリパラメータを取得する

## まとめ

- 全て取得するには`$request->all()`を使う
  - キーバリューのペアが配列で返ってくる
- 1つ取得する場合
  - `query`メソッドを使う
  - 第2引数にデフォルト値を指定できたりする
  - 存在しない場合は`null`が返ってくる(多分)
- Requestクラスのその他のメソッド
  - メソッドによってクエリストリングとリクエストボディの優先度が違う

|メソッド|優先度|
|-|-|
|`query`|クエリストリングのみ|
|`get`|クエリストリング→リクエストボディ|
|`input`|リクエストボディ→クエリストリング|
|動的プロパティ|`input`と同じ?|

## 参考

- [Requestの各メソッド（query(), get(), all()...）の使い分け - Qiita](https://qiita.com/piotzkhider/items/feaba3acda27d2e432d8)
