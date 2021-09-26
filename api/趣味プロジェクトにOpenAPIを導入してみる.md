# 趣味プロジェクトにOpenAPIを導入してみる

OpenAPI定義ファイルはYAMLまたはJSONで書く必要があるが、量が多く文法も覚えないといけないので結構厳しい。そこで`Stoplight Studio`というツールを使ってAPIを定義する。`Stoplight Studio`を使うとGUIでOpenAPI定義ファイルを作成することが出来る。

作成したOpenAPI定義ファイルからモックサーバーを起動するには、`Prism`を使う。`Prism`は`Stoplight Studio`と同じStoplight社が開発している（`Stoplight Studio`にも内蔵されている）。

モックサーバーの主な用途はフロントエンドで動作確認に使うことなので、`Prism`はフロントエンド側にnpmで入れて使用する。

## 参考

- [本当に使ってよかったOpenAPI (Swagger) ツール | フューチャー技術ブログ](https://future-architect.github.io/articles/20191008/)
- [OpenAPIからモックサーバを建てられるPrismを実際のプロジェクトに導入してみた | フューチャー技術ブログ](https://future-architect.github.io/articles/20210410/)
