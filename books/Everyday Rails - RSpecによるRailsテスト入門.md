# Everyday Rails - RSpecによるRailsテスト入門

## 3章 モデルスペック

### be_validマッチャ

`be_〇〇`というメソッドは、オブジェクトに対して`〇〇`というメッセージを送って、その結果が`true`かどうかを検証しているのかなと思いました。

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

Everyday Railsは簡単なバリデーションに対してもテストを書くべきと書いてあります。理由はバリデーションの追加について忘れていた場合でも気付くことができるためです。

DSLに対するテストは書かなくてもよいという意見もあります。DSLに対するテストというのは、例えば`validate :name, precense: true`に対して、`name`が`nil`だとバリデーションが失敗することのテストなどです。何故かというと、 DSLが正しく動くことに関してはRailsに責任があるためです。

2つの意見をまとめると、まずはビジネスロジックに対するテストを重点的に書くべき。バリデーションなどに対するテストは、手間がかからないのであれば書いたほうがよいが、ビジネスロジックに対するテストと比較すると重要ではないということだと思います。

バリデーションに対するテストは、Railsになれていないうちは積極的に書いていったほうが良いと思います。また、単純でないテストのバリデーションから書いていけば良いと思います。例えば、`ユーザーは同じ名前のプロジェクトを作れない`というのは、先述のバリデーションより複雑なので、こちらから書くべきです。

### before each、before contextの使い分け

> before(:all) と before(:suite) は時間のかかる独立したセットアップ処理を1回だけ実行し、テスト全体の実行時間を短くするのに役立ちます。ですが、この機能を使うとテスト全体を汚染してしまう原因にもなりかねません。可能な限り before(:each) を使うようにしてください。

とあります。テストの各exampleは独立させるという考え方があるので、それに従うとbefore(:each)を使ったほうが良いです。なぜテストの各exampleを独立させるべきかというと、1番の理由は依存があると前のテストケースの影響を受けてしまうからです（本書の汚染はこの意味）。やったことがないので分かりませんが、テストを並列実行しやすいというのもあるかもしれません。

## 4章 FactoryBotを用いたテストデータの作成

### ファクトリの重複を減らすための方法（継承とトレイト）

```ruby
# 継承を使った場合
FactoryBot.define do
  factory :project do
    sequence(:name) { |n| "Project #{n}" }
    description "A test project"
    due_on { 1.week.from_now }
    owner { association :user }

    factory :project_due_today do
      due_on { Time.current }
    end
  end
end

FactoryBot.create(:project_due_today)

# トレイトを使った場合
FactoryBot.define do
  factory :project do
    sequence(:name) { |n| "Project #{n}" }
    description "A test project"
    due_on { 1.week.from_now }
    owner { association :user }

    trait :due_today do
      due_on { Time.current }
    end
  end
end

FactoryBot.create(:project, :due_today)
```

この例であれば、FactoryBotの継承とトレイトの違いは、ファクトリを生成するときの指定方法くらい。トレイトは複数指定できて柔軟なので、基本的にはトレイトを使うのが良いと思う。他にも便利な機能があるので（transientとか）、ファクトリの定義で困った場合はFactoryBotのドキュメントを読む。

## 7章 リクエストスペックを用いたAPIのテスト

## 8章 スペックをDRYに保つ

サポートモジュール
  共通する処理をモジュールに切り出す

shared_context
  テストのセットアップ（letやbefore）を共通化する

カスタムマッチャ
  独自のマッチャを定義する

aggregate_failures
  エクスペクテーションが失敗した場合も複数実行できるようにする

## 参考

- [Rails 開発で意識していること 1 · ryym.log](https://ryym.tokyo/posts/my-rails-practice1/)
- [Factory Bot Documentation](https://github.com/thoughtbot/factory_bot/blob/master/GETTING_STARTED.md)
