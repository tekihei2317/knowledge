# UUIDの生成方法

## UUIDとは何か

重複しないような値のこと。何種類かあるみたい。

## 生成方法

`Str::uuid()`を使う。この関数はオブジェクトを返すので、使用するときは文字列に変換する。

```php
>>> $uuid = Str::uuid();
=> Ramsey\Uuid\Lazy\LazyUuidFromString {#3648
     uuid: "041a945d-e9f9-4e7e-8544-9701fbd30df8",
   }
>>> $uuid->toString();
=> "041a945d-e9f9-4e7e-8544-9701fbd30df8"
```

`Str::uuid()`はUUIDのバージョン4を生成する。UUIDのバージョン4の長さは、16進数の文字列32 Byte + 境界文字(-)4 Byteの36Byteになるらしい。

## 参考
