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

- php://stdoutとphp://outputの違い
  - [php - does echo equal fputs( STDout )? - Stack Overflow](https://stackoverflow.com/questions/7027902/does-echo-equal-fputs-stdout)
- Eloquentのfirstメソッド（最初の1件を取得）がどこに実装されているかが分からない
- Requestのqueryメソッドがどこから取得しているかが分からない
  - InteractsWithInputトレイトに実装があるみたい
  - $queryというプロパティにアクセスしているように見えるけど、それがRequestクラスになさそう
