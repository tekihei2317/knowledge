# LivewireでEloquentモデルにバインドする方法

- 例えばフォームに入力した値をリアルタイムに変数に反映したい場合

## 基本

### 変数へのバインド

- 変数名はキャメルケースからケバブケースに変換する

### 配列へのバインド

- ドット(.)でつなげて書く

## モデルへのバインド

- 配列の場合と同じように書く
- バリデーションの条件を指定しないとおかしくなるので注意する
  - 変数の値が反映されない
  - 通信が発生したときに値がリセットされる
