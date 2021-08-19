# Eloquentで簡易検索機能の実装

## 実装例

```php
$query = User::query();
$conditions = $this->filterConditions;

if ($conditions['id'] !== null && $conditions['id'] !== '') {
    $query = $query->where('id', $conditions['id']);
}
if ($conditions['name'] !== null && $conditions['name'] !== '') {
    $query = $query->where('name', 'like', "%{$conditions['name']}%");
}

return $query->get();
```

### ポイント

- `Model::query`でEloquentビルダー(`Illuminate\Database\Eloquent\Builder`)を取得する
- フォームに何も入っていない状態は、nullまたは空文字列かどうかで判定
  - 初期値をnullにしているが、フォームに入力してから空にすると空文字列になったため
- 文字列の中の変数展開は`"{変数}"`で出来る

## 参考

- [PHPで文字列リテラルに式展開 - Qiita](https://qiita.com/tadsan/items/e4796449c736cfb5c9bd)
