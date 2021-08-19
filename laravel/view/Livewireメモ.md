# Livewireメモ

- ビューコンポーネントのルート要素は1つでなければいけない

```html
<!-- OK -->
<div>
  <h1>Hello, world!</h1>
</div>

<!-- NG -->
<div>
  <h1>Hello, world!</h1>
</div>

<h1>Hello, world!</h1>
```

- バリデーションルールが無いとデータバインディングが出来ない
- @livewireScriptsは何をしているのか
- バインドしている値を確認したい
  - 画面に表示して確認すれば良さそう
- コントローラーを経由してたけどその必要無さそうな気がしてきた
  - Livewireのコンポーネントに直接マウントしてパラメータを渡せるみたい
  - コントローラーみたいに使えるよって書いてありますね
    - [Rendering Components | Laravel Livewire](https://laravel-livewire.com/docs/2.x/rendering-components#page-components)
