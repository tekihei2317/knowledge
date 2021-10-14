# Code Climate CLIを使ってみる

ソースコードを公開出来ない事情があったため、Code ClimateのSaaS版を使うことが出来なかった。そのため、Code Climate CLIを使って欲しい値が取得できるかを調査した。

欲しい値は以下。

- REMEDIATION TIME
  - 技術的負債の返済までにかかる時間の目安。リファクタリングのKPIとして用いる。
- ファイルごとのREMEDIATION TIME
  - SaaS版ではmaintainabilityという表記だった。リファクタリングの優先度をつけるために用いる。
- ファイルの変更回数
  - これは`git log`で取得できる。これもリファクタリングの優先度をつけるために用いる。
- PRごとのREMEDIATION TIMEの変化
  - GitHub APIと組み合わせて使う必要がある気がする。REMEDIATION TIMEが取得できれば計算できると思う。

## cliを試す

結論としては、REMEDIATION_TIMEは取得できなかったが、代わりにremediation pointsという値が取得できた。remediation pointsはコードの問題点をスコア化したもので、ドキュメントによると、ファイルのremediation pointsに応じて以下のようにランク付けさられるらしい（[参考](https://docs.codeclimate.com/docs/code-climate-glossary#remediation)）。

| Remediation Points | File Rating |
| ------------------ | ----------- |
| 0 - 2M             | A           |
| > 2M - 4M          | B           |
| > 4M - 8M          | C           |
| > 8M - 16M         | D           |
| > 16M              | F           |

### インストール

`homebrew`でインストールできる。

```bash
brew tap codeclimate/formulae
brew install codeclimate
```

### 分析の実行

`codeclimate analyze`で分析ができる。フォーマットはtext、html、jsonから選択できる。

#### テキストの場合

```bash
codeclimate analyze
```

結果

```bash
Starting analysis

== app/controllers/users_controller.rb (1 issue) ==
8-47: Method `progress` has 31 lines of code (exceeds 25 allowed). Consider refactoring. [structure]

== app/models/user.rb (3 issues) ==
14-28: Method `find_for_oauth` has a Cognitive Complexity of 7 (exceeds 5 allowed). Consider refactoring. [structure]
97-115: Method `scrape_first_results` has a Cognitive Complexity of 6 (exceeds 5 allowed). Consider refactoring. [structure]
117-135: Method `scrape_retry_results` has a Cognitive Complexity of 6 (exceeds 5 allowed). Consider refactoring. [structure]

Analysis complete! Found 4 issues.
```

#### HTMLの場合

```bash
codeclimate analyze -f html
```

[![Image from Gyazo](https://i.gyazo.com/1db2c56e69dc10dd0cb88b5fe9f45704.png)](https://gyazo.com/1db2c56e69dc10dd0cb88b5fe9f45704)

#### JSONの場合

```bash
codeclimate analyze -f json
```

以下のようなjsonが生成された。`type="issue"`のものが問題点を表している。

```json
[
  {
    "name": "javascript.parse.succeeded",
    "type": "measurement",
    "value": 6,
    "engine_name": "structure"
  },
  {
    "engine_name": "structure",
    "fingerprint": "e1ed45bd05e49d9c5d087bfb08494848",
    "categories": ["Complexity"],
    "check_name": "method_lines",
    "content": { "body": "" },
    "description": "Method `progress` has 31 lines of code (exceeds 25 allowed). Consider refactoring.",
    "location": {
      "path": "app/controllers/users_controller.rb",
      "lines": { "begin": 8, "end": 47 }
    },
    "other_locations": [],
    "remediation_points": 744000,
    "severity": "minor",
    "type": "issue"
  },
  // (省略)
]
```

jqで頑張って目的の値を取得してみた（~~結局JSでやることになりそうなのでここに供養します~~）。

すべてのファイルの`remediation_points`の合計

```bash
cat result.json | jq 'map(select(.type=="issue")) | map(.remediation_points) | add'
#=> 1594000
```

ファイルごとの`remediation_points`の合計

```bash
cat result.json | jq 'map(select(.type == "issue")) | map({path: .location.path, points: .remediation_points}) | group_by(.path) | map({path: (.[0].path), points: ([.[].points]|add)})'
#=> [{ "path": "app/controllers/users_controller.rb", "points": 744000 }, { "path": "app/models/user.rb", "points": 850000 }]
```

## どうやって可視化するか

サーバーが用意できなかったので、以下のようにして可視化しようと思っている。

1. GitHub Actionsで、Code ClimateのDockerイメージを使ってJSONを生成する
2. 生成したjsonを、GASで作ったAPIにPOSTする
3. GASでjsonから目的の値を計算して、スプレッドシートに書き込む

TODO: やってみる

## 参考

- [生産性・技術的負債をMetabaseで可視化した話 - LIFULL Creators Blog](https://www.lifull.blog/entry/2021/01/20/195106)
  - `Metabase`がめっちゃカッコよかったのでやりたくなった。
- [codeclimate/codeclimate: Code Climate CLI](https://github.com/codeclimate/codeclimate)
- [jq コマンドを使う日常のご紹介 - Qiita](https://qiita.com/takeshinoda@github/items/2dec7a72930ec1f658af#map)
- [jqコマンドでJSONのキーの集計(キーの数・合計・平均・最大・最小等を求める)を行う | 俺的備忘録 〜なんかいろいろ〜](https://orebibou.com/ja/home/201605/20160509_001/)
  - `jq`の`map`や`group_by`の使い方が分かりやすかった。
