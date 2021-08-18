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
