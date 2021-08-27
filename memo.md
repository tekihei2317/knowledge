# メモ

## ブログのネタ

- Livewireで応募フォームを作る

## 疑問点

- プロパティ名に変数が使えるのかな?
  - $sourceは'query'や'headers'などの文字列

```php
// Illuminate\Http\Conserns\IntaractsWithInput

protected function retrieveItem($source, $key, $default)
{
    if (is_null($key)) {
        return $this->$source->all();
    }

    return $this->$source->get($key, $default);
}
```
