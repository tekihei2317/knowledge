# alpの使い方

## alpとは

Webサーバーのアクセスログを解析するツール。ボトルネックを見つけるのに使う。

## 使い方

Nginxを使うので、Nginxの場合の設定方法のメモ。

- ログフォーマットの形式をLTSVまたはJSONに変更する
  - JSONでも解析できるみたい
  - Nginxの設定を再読み込みは`nginx -s reload`で出来る
- コマンドを組み立てる
  - `cat access.log | alp json`が基本形
  - URLに含んでいるIDをまとめるために`-mオプション`を使う
    - 正規表現でまとめるURLを指定する
    - 複数指定する場合はカンマ区切りで指定できる
- alpの結果を観察する
  - 平均（AVG）が重いやつから改善すれば良い（事前研修より）

### コマンドの例

```bash
cat alp/sample.log | alp json -m '/api/chair/[0-9]+,/api/estate/[0-9]+,api/recommended_estate/[0-9]+' --sort avg -r
```

## 参考

- [alpの使い方(基本編)](https://zenn.dev/tkuchiki/articles/how-to-use-alp)
  - こことREADME見れば何とかなりそうです
