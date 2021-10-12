# Terserを使ってみる

terserがNuxtのHMRのパフォーマンス低下の原因になっているっぽかったので、まずはterserについて理解することにした。問題になっていた設定は以下。

```js
// nuxt.config.js
const TerserPlugin = require("terser-webpack-plugin");
module.exports = {
  build: {
    optimization: {
      minimize: true,
      minimizer: [
        new TerserPlugin({
          sourceMap: false,
          parallel: true,
          extractComments: { filename: "LICENSES" },
          terserOptions: {
            compress: {
              drop_console: process.env.NODE_ENV === "production"
            },
            output: {
              comments: /^\**!|@preserve|@license|@cc_on/
            }
          }
        })
      ]
    },
  }
}
```

ここのoptimizationのところをコメントアウトすると、ホットリロードの速度(5回平均)が以下のように改善した。

|        | コメントアウト前 | コメントアウト後 |
| ------ | ---------------- | ---------------- |
| Server | 4.6s             | 1.4s             |
| Client | 1.3s             | 0.6s             |

[terser-webpack-plugin](https://github.com/webpack-contrib/terser-webpack-plugin)は、Webpackからterserを使うためのもの。terser-webpack-pluginに渡したプロパティはそのままterserに渡していると思うので、terserの対応するプロパティを見ていく。

## Terserとは何か

JavaScriptのminifyを行うライブラリ。昔はUglifyJSというminifierが使われていたが、ES6の文法（let/const、アロー関数、分割代入等）に対応していなかったため、別ブランチでES6対応版の[uglify-es](https://www.npmjs.com/package/uglify-es)が開発されていた。uglify-esが開発終了したため、それをForkしてterserが作られた。

npmのトレンドを見ると、現在はTerserがUglifyJSを追い抜いていた。
[terser vs uglify-es vs uglify-js | npm trends](https://www.npmtrends.com/terser-vs-uglify-js-vs-uglify-es)

圧縮にも色々ある

## 参考資料

- [イマドキは Uglify JS じゃなくて Terser だ！Terser を使ってみる - Neo's World](https://neos21.net/blog/2020/09/03-02.html)
- [個人的にTerser & Babelの好きなところ](https://gist.github.com/shqld/d101cae50dd83ab7d3487cdb10b80f4d)
