# JavaScriptの!!（ビックリマーク2つ）について

条件式に指定したときに真とみなされる値をTruthyな値、反対に偽とみなされる値のことをFalsyな値と言います。

JavaScriptでFalsyな値は `false` / `null` / `undefined` / `NaN` / `0` / `""` の6つです。

| Falsyな値            |
| -------------------- |
| false                |
| null                 |
| undefined            |
| NaN                  |
| 0                    |
| 空文字列（"",'',``） |

論理否定（!）を使用すると、Truthyな値は`false`に、Falsyな値は`true`に変換されます。つまり、二重の論理否定（!!）を使うとTruthyな値は`true`に、Falsyな値は`false`に変換されます。

```javascript
// Falsyな値に二重の論理否定（!!）を使う
> falsyList = [false, null, undefined, NaN, 0, ""]
[ false, null, undefined, NaN, 0, '' ]
> falsyList.map((item) => !!item)
[ false, false, false, false, false, false ]

// Truthyな値に二重の論理否定（!!
> truthyList = [true, 1, "string", [3, 1, 4], { test: 'test' }]
[ true, 1, 'string', [ 3, 1, 4 ], { test: 'test' } ]
> truthyList.map((item) => !!item)
[ true, true, true, true, true ]
```

if文の中で二重の論理否定を使っている箇所があったので、これは不要だと気づきました。

## 参考

- [Falsy (偽値) - MDN Web Docs 用語集: ウェブ関連用語の定義 | MDN](https://developer.mozilla.org/ja/docs/Glossary/Falsy)
- [論理否定 (!) - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Logical_NOT)
