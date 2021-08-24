# Fakerの使い方

- いずれかの要素
  - `randomElement`、`randomElements`が使える

```php
echo $faker->randomElement(['a', 'b', 'c', 'd', 'e']);

// 'c'

echo $faker->randomElements(['a', 'b', 'c', 'd', 'e']);

// ['c']

echo $faker->randomElements(['a', 'b', 'c', 'd', 'e'], 3);

// ['a', 'd', 'e']
```

## 参考

- [FakerPHP / Faker](https://fakerphp.github.io/)
- [LaravelのFakerを日本語化する - Qiita](https://qiita.com/kazuhei/items/5d33eedb9ebdd62e0bfb)
