# ドメインごとにルーティングを分ける

## 方針

Route::domainを用いて、そのドメインでのみ有効なドメインを定義する。

## やり方

`routes/admin.php`を作成して、管理画面用のルーティングを書く。
`RouteServiceProvider`で、ユーザー画面用のルーティングと管理画面のルーティングを登録する。

```php
// app/Providers/RouteserviceProvider
$this->routes(function () {
    Route::domain(config('app.admin_domain'))
        ->middleware('web')
        ->namespace($this->namespace)
        ->group(base_path('routes/admin.php'));

    Route::domain(config('app.domain'))
        ->middleware('web')
        ->namespace($this->namespace)
        ->group(base_path('routes/web.php'));
});

// config/app.php
'domain' => env('APP_DOMAIN', 'localhost'),
'admin_domain' => env('APP_ADMIN_DOMAIN', 'admin.localhost'),

// .env（開発環境）
APP_DOMAIN=localhost
APP_ADMIN_DOMAIN=admin.localhost
```

localhostにサブドメインをつけることができるので、開発環境では`localhost`と`admin.localhost`を使うことにしました。

## 説明

ルーティングの登録は`app/Providers/RouteServiceProvider.php`で行われている。

```php
// 登録処理
$this->routes(function () {
    Route::prefix('api')
        ->middleware('api')
        ->namespace($this->namespace)
        ->group(base_path('routes/api.php'));

    Route::middleware('web')
        ->namespace($this->namespace)
        ->group(base_path('routes/web.php'));
});
```

Route::domainを使うと、そのドメインのときのみに有効になるルーティングを設定できる（完全一致?、要検証）

```php
// app/Providers/RouteserviceProvider
$this->routes(function () {
    // example.comでもみ有効
    Route::domain('example.com')
        ->middleware('web')
        ->namespace($this->namespace)
        ->group(base_path('routes/admin.php'));
});
```

## 参考

- [laravelでrouteにdomainを指定した場合のfeatureテスト方法 - もがき系プログラマの日常](https://kojirooooocks.hatenablog.com/entry/2019/08/03/033209)
  - Route::groupでドメインを指定できるみたい。こっちのほうが簡単そう。
