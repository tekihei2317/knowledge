# Livewireで数値をバインドするときにつまった

floatで型宣言をしていた
空文字のときにエラーが出る
型宣言を辞めた
バリデーションで弾くrequired, numeric
inputはtype=number以外にしたほうが良いかもしれない
  全角数字が入力出来ない
  あまり意味のない
SQLを実行するときに数値に変更してくれている?
数値型のカラムに文字列を入れても問題ない?

## 参考

- [数値入力で input[type="number"]を使ったら、ユーザから問い合わせが増えてしまった話 - Qiita](https://qiita.com/diescake/items/65ce4499ab8a70d029de)
  - input[type=number]を使う基準の1つは、スピンボックスが表示されることに意味があるかどうか
