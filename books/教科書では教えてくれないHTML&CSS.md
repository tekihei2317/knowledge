# 教科書では教えてくれないHTML&CSS

## 3章

## 4章 ヘッダー

### ナビゲーションのアニメーションの実装

`height`に対して`transition`を適用することで、スライドダウン・スライドアップを表現できる。あふれた子要素がはみ出ないように、`overflow: hidden`をつけることに注意する。

TODO: CodePen

`height`が`auto`の場合は`transition`が反応しないため、`height`に値を設定する必要がある。固定値ではない場合は、JavaScriptで計算してスタイルを当てるしかない気がする。

## 5章 フッター

### マージンの相殺

上下に隣接する兄弟要素にマージンが設定されているとき、大きい方のマージンが適用されること。左右の場合はマージンの相殺は起きない。

マージンの相殺を利用したテクニックがある。例えば`.container > *`に`margin: 30px 0`と設定すると、`.container`の直下の要素を全て30pxにする事ができる。今思ったけどこれmargin-topだけで良くないか。

左右のマージンが相殺しないことも利用できる。例えば全部の要素に20pxの間隔を開けたい場合は、`margin: 0 10px`と半分のマージンを設定する。これｈフレックスボックスの、`justify-content: space-around`に相当する。

## 参考

- [width、heightがautoの要素にtransitionを適用する - メモを揉め](https://memowomome.hatenablog.com/entry/2016/08/03/080000)
