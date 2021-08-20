# ISUCONのオペレーション技術の基本

## ISUCONのスコアについて

- Dev(アプリケーションの改善)→スコアを伸ばす
- Ops(環境構築等)→スコアを守る(スコアが伸びる土台を作る)

## オペレーションでやること

- SSH出来るようにする
- リポジトリをGitで管理する
- ローカルで動かせるようにする
  - 動かせなかった場合はVSCode Remote SSHかな...
- デプロイの自動化
- ボトルネック解析
  - とりあえずalpを使っておけば良さそう
  - nginxのアクセスログ→alp
  - MySQLのスロークエリログ→pt-query-digest
  - プロファイリング(どのプロセスが時間を取っている(?)→blackfire.io

## メモ

- 色々な方法があるんだなぁとちょっとビックリ
- ローカルで動かす人と動かさない人がいるみたい
  - 変更→pushで確認は大変そう
  - でもローカルで動かせるようにするのも大変そう
- なんじゃこれ
  - [https://highloadcup.ru/en/](https://highloadcup.ru/en/)
- これをやってみたい
  - [https://blog.yuuk.io/entry/linux-server-operations](https://blog.yuuk.io/entry/linux-server-operations)

## 参考

[ISUCON予選突破を支えたオペレーション技術 - ゆううきブログ](https://blog.yuuk.io/entry/web-operations-isucon)

[ISUCON8予選 序盤環境構築覚え書き](http://tatamo.81.la/blog/2018/09/16/isucon8-qual-2/)

[プロファイラを使った PHPアプリケーション改善の勘所 - Innovator Japan Engineers' Blog](https://innovator-japan.hatenablog.com/entry/2019/01/31/121731)

[ISUCON7予選の上位陣の戦略まとめ - Bit Journey's Tech Blog](https://blog.bitjourney.com/entry/2017/11/09/101740)
