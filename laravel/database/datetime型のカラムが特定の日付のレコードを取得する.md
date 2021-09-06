# datetime型のカラムが特定の日付のレコードを取得する

SQLの日付の関数は、RDBMSによって違うのであまり使いたくない（RDBMSが変わることはあまりないのでそんなに気にしなくていいと思うけど）。

Laravelにはクエリビルダに`whereDate/whereMonth/whereYear/whereTime`などのメソッドが用意されているので、それらを使えばよい。おそらくこれがRDBMSによる違いを吸収してくれている。

## whereDate

使用例

```php
$users = DB::table('users')
  ->whereTime('created_at', '=', '11:20:45')
  ->get();
// Carbonのインスタンスも渡せる
$users = DB::table('users')
  ->whereTime('created_at', '=', Carbon::today())
  ->get();
```

実装はこんな感じになっていて、`DateTimeInterface`クラス?を実装しているクラスのインスタンスを渡すこともできる。

```php
public function whereDate($column, $operator, $value = null, $boolean = 'and')
{
    [$value, $operator] = $this->prepareValueAndOperator(
        $value, $operator, func_num_args() === 2
    );

    $value = $this->flattenValue($value);

    if ($value instanceof DateTimeInterface) {
        $value = $value->format('Y-m-d');
    }

    return $this->addDateBasedWhere('Date', $column, $operator, $value, $boolean);
}
```

## 参考

- [Database: Query Builder - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/8.x/queries)
- [Laravel 特定の日付・時間のデータ取得にはCarbonとwhereDateを使おう | 40代からプログラミング！](https://biz.addisteria.com/laravel_carbon/)
  - Carbonのインスタンス渡しても出来るみたい
