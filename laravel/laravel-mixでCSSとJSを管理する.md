# laravel-mixでCSSとJSを管理する

## CSSの管理

Sassはブラウザが直接読み込むことはできないので、CSSにコンパイルする必要がある。Laravelではlaravel-mix（webpackのラッパー）を用いてCSSやJSをコンパイルする。

通常のCSSファイルの場合でも圧縮したほうが良いので（要出典）、`public/`ディレクトリに直接置くのではなく、`resources/`に置いてlaravel-mixに乗せてあげたほうが良い。

SCSSファイル

```scss
// resources/css/test.scss

.parent {
  .child {
    background-color: #eee;
  }
}
```

laravel-mixの設定ファイル

```js
// webpack.mix.js

// resources/css/test.scss → public/css/test.scssにコンパイルする
mix.sass("resources/css/test.scss", "public/css");
```

読み込む側(Blade)

TODO: mixメソッドについて

```html
<link rel="stylesheet" href="{{ asset('css/test.css') }}">
```

## JSの管理

全てのファイルをまとめたほうが良いのか。
ページごとに読み込むファイルが違う場合はどうするのか。
jQuery等のライブラリを使っている場合はどうするのか。npmでインストールしてrequireすれば良いのか。
minifyだけすることも出来る。jsメソッドを使うとトランスパイル等が走っておかしくなることがある。

## 参考

- [Sass Preprocessing | Laravel Mix Documentation](https://laravel-mix.com/docs/6.0/sass)
