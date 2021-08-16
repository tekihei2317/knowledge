# Livewireの基本

- ajaxリクエストでデータを更新する
- データはPHPのクラスのパブリック変数で持つ
- DOMを更新する際は、要素にIDを付けて差分だけ更新するようになっている?

## コンポーネントの作成

```bash
# ケースはキャメルケースでもケバブケースでも可
php artisan make:livewire TestComponent
php artisan make:livewire test-component

# 階層構造は.や/で表現する
php artisan make:livewire TestNs/TestComponent
php artisan make:livewire test-ns.test-component
```

## コンポーネントの使用

- HTMLに@livewireディレクティブを書く
- @livewireディレクティブはクラスを呼ぶ
  - `@livewire('test-ns.test-component')`とすると、`App\Http\Livewire\TestNs\TestComponent`が呼ばれる
  - クラスがないとコンポーネントが無いよというエラーが出る

## 参考

- [Laravel8でLivewireの使い方を学ぶ | アールエフェクト](https://reffect.co.jp/laravel/laravel-livewire)