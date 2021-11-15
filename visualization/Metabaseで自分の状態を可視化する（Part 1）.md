# Metabaseで自分の状態を可視化する（Part 1）

最近はプログラミングばかりやっている。その原因はコードを書けばGitHubに草を生やせるが（ほぼ毎日見ている）、生活をしても効果が確認できないからだと考えた。GitHubの草のように、自分の健康状態などを確認できるダッシュボードがあれば良いと思ったので、作ってみることにした。

可視化には以前から気になっていたMetabaseを使ってみようと思っている。まずは可視化したい項目を洗い出す。

## 計測したい情報

### 健康

- 歩数
- 睡眠時間

歩数と睡眠時間の計測にはスマートウォッチを用いる。APIを検索するとFitbitの情報が出てきたが、Fitbitは安いものでも1万円くらいと高かったため、[Xiaomi Mi スマートバンド6](https://www.amazon.co.jp/%E3%80%90%E6%97%A5%E6%9C%AC%E6%AD%A3%E8%A6%8F%E4%BB%A3%E7%90%86%E5%BA%97%E5%93%81%E3%80%91Xiaomi-1-56%E3%82%A4%E3%83%B3%E3%83%81%E3%83%87%E3%82%A3%E3%82%B9%E3%83%97%E3%83%AC%E3%82%A4-14%E6%97%A5%E9%96%93%E3%81%AE%E3%83%90%E3%83%83%E3%83%86%E3%83%AA%E3%83%BC%E6%8C%81%E7%B6%9A%E6%99%82%E9%96%93-%E7%A8%AE%E9%A1%9E%E3%82%A8%E3%82%AF%E3%82%B5%E3%82%B5%E3%82%A4%E3%82%BA%E3%83%A2%E3%83%BC%E3%83%89-LINE%E3%83%BB%E3%83%A1%E3%83%83%E3%82%BB%E3%83%BC%E3%82%B8%E3%83%BB%E7%9D%80%E4%BF%A1%E3%83%BB%E5%BA%A7%E3%82%8A%E3%81%99%E3%81%8E%E9%80%9A%E7%9F%A5/dp/B097918L2C/ref=sr_1_14_sspa?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&dchild=1&keywords=fitbit&qid=1634997729&s=electronics&sr=1-14-spons&psc=1&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUEyNDUxOFE1UzhNNzVOJmVuY3J5cHRlZElkPUEwOTQ3MDk3RThKMVlEMTk4UEtKJmVuY3J5cHRlZEFkSWQ9QTFHNzlEUkxSSUtSUFUmd2lkZ2V0TmFtZT1zcF9tdGYmYWN0aW9uPWNsaWNrUmVkaXJlY3QmZG9Ob3RMb2dDbGljaz10cnVl)（約6000円）を購入した。こちらもAPIがありそうだったのと、APIが使用できなかった場合でもGoogle Fitと連携してGoogle Fit APIから取得すればよいので大丈夫だと考えた。

### 生産性

- GitHubのコントリビューション
- GitHubの変更したコード行数
- コーディング時間（WakaTime）
- ブログの記事数
- メモ用のGitHubリポジトリの活動状況

### その他

- 読書時間（Kindle）
- 読書冊数（Kindle）
- 出費・貯蓄（Money Forward）

本は大体Kindleで読んでいるためKidnleから取得しようと思っている。紙の本も借りたり買ったりするため、そこは別途対応が必要そう。

### やってみたい

- 集中している時間（JINS MEMEなど）
