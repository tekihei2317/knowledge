# メモ

## ブログのネタ

- Livewireで応募フォームを作る

## 勉強会の発表内容

- Livewire
  - たのしい
- クエリビルダを作った
  - 作っている
- RDBMSのインデックスを理解する
  - どういう場面で生きるか(where狙い、order by狙い)
  - 計測してみる
- SQLを勉強できるアプリを作った
  - これから
- ISUCON
  - パフォーマンスの計測方法

## memo

- モデルのプロパティをtrue/falseで取得したい
  - nullはnull、0をfalse、1をtrueで取得したい
  - $castsで指定すれば良さそう
- systemctlのlist-unitsとlist-unit-filesの違い
- ブラウザの仕組み、JSのフレームワーク(React/Vue)がそれらをどのように扱っているか
  - 生のJSでイベントを扱おうとすると全然分からなかった

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
- Content Security Policyとは
