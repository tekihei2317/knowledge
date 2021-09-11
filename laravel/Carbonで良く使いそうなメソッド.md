# Carbonで良く使いそうなメソッド

こういうことしたいな〜と思ったら、大体のことは用意されていると思う。

## インスタンスの取得

```php
// 現在時刻
>>> Carbon::now();
=> Carbon\Carbon @1631335790 {#2606
     date: 2021-09-11 04:49:50.670118 UTC (+00:00),
   }
// 年月日時を指定して作成(第一引数以外は省略可能)
>>> Carbon::create(2025, 1, 2, 3, 4, 5);
=> Carbon\Carbon @1735689600 {#2618
     date: 2025-01-02 03:04:05.0 UTC (+00:00),
   }
// 年月日を指定して作成(時刻は現在の時刻になる)
>>> Carbon::createFromDate(2025, 1, 1);
=> Carbon\Carbon @1735707011 {#2604
     date: 2025-01-01 04:50:11.063007 UTC (+00:00),
   }
// 時刻を指定して作成(日付は現在の日付になる)
>>> Carbon::createFromTime(12, 30);
=> Carbon\Carbon @1631363400 {#2617
     date: 2021-09-11 12:30:00.0 UTC (+00:00),
   }
// 今日の0時
>>>Carbon::today();
=> Carbon\Carbon @1631318400 {#2609
     date: 2021-09-11 00:00:00.0 UTC (+00:00),
   }
// 明日の0時
>>> Carbon::tomorrow();
=> Carbon\Carbon @1631404800 {#2602
     date: 2021-09-12 00:00:00.0 UTC (+00:00),
   }
// 昨日の0時
>>> Carbon::yesterday();
=> Carbon\Carbon @1631232000 {#2611
     date: 2021-09-10 00:00:00.0 UTC (+00:00),
   }
```

## 文字列への変換

```php
// 現在の年月日時
>>> $date->toDateTimeString();
=> "2021-09-11 04:55:35"
// 現在の年月日
>>> $date->toDateString();
=> "2021-09-11"
// 現在の時刻
>>> $date->toTimeString();
=> "04:55:35"
```

## 比較

```php
// < (less than)
>>> $today->lt($tomorrow);
=> true
>>> $today->lessThan($tomorrow);
=> true
>>> $today->lt($today);
=> false
// <= (less than or equal to)
>>> $today->lte($tomorrow);
=> true
>>> $today->lessThanOrEqualTo($tomorrow);
=> true
>>> $today->lte($today);
=> true
```

## 参考

- [Carbon - A simple PHP API extension for DateTime.](https://carbon.nesbot.com/docs/)
- [全217件！Carbonで時間操作する実例 – console dot log](https://blog.capilano-fw.com/?p=867#create)
