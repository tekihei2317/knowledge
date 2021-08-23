# datetimeをdateで絞り込む

## 問題

- `datetime`型のカラム`access_time`がある
- これを開始日`start_date`と終了日`end_date`（両端点を含む）で絞り込むにはどうすればよいか
  - `start_date`の00:00:00から、`end_date`の23:59:59まで

## 考察

- `datetime`と`date`を比較することが出来る
  - このとき、`date`はその日の最初の時間（00:00:00）とみなされる（はず）
  - なので、`start_date <= access_time < end_date + 1`で比較すればよい
  - 日付の加算はDBMSに依存しそうなので、PHPでやったほうが良さそう（Carbonを使う）

## 実装

```php
$query = AccessLog::query();
extract($this->filterConditions); // $filterConditionsは、start_dateとend_dateをキーに持つ配列

if ($startDate !== '') {
    $query->where('access_time', '>=', $startDate);
}
if ($endDate !== '') {
    # datetimeと比較するので、1日足して<で比較する
    $endDate = (new Carbon($endDate))->addDay()->format('Y-m-d');
    $query->where('access_time', '<', $endDate);
}

$result = $query->get();

```

## 参考

- [yoo-s.com](https://yoo-s.com/topic/detail/788)
  - 取得するときにCarbonで返すことが出来るみたい
