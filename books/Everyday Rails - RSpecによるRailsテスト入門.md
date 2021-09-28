# Everyday Rails - RSpecによるRailsテスト入門

## 3章 モデルスペック

### be_validマッチャ

```ruby
user = User.new(
  first_name: "test",
  last_name: "taro",
  email: "taro@example.com",
  password: "password",
)

# 以下は同義?
expect(user).to be_valid
expect(user.valid?).to eq true
```

### バリデーションのテストはどれくらい書くべきか

Everyday Railsは簡単なバリデーションに対してもテストを書くべきと書いてある。理由はバリデーションの追加について忘れていた場合でも気付くことができるため。

DSLに対するテストは書かなくてもよいという意見もある。DSLに対するテストというのは、例えば`validate :name, precense: true`に対して、`name`が`nil`だとバリデーションが失敗することのテストなど。何故かというと、 DSLが正しく動くことに関してはRailsに責任があるため。

2つの意見をまとめると、まずはビジネスロジックに対するテストを重点的に書くべき。バリデーションなどに対するテストは、手間がかからないのであれば書いたほうがよいが、ビジネスロジックに対するテストと比較すると重要ではないということだと思う。

バリデーションに対するテストは、Railsになれていないうちは積極的に書いていったほうが良いと思う。また、単純でないテストのバリデーションから書いていけば良いと思う。例えば、`ユーザーは同じ名前のプロジェクトを作れない`というのは、先述のバリデーションより複雑なので、こちらから書くべき。

## 参考

- [Rails 開発で意識していること 1 · ryym.log](https://ryym.tokyo/posts/my-rails-practice1/)
