---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
---

# Metabaseで個人ダッシュボードを作成する

---

# Metabaseとは

- オープンソースのデータ可視化ツール
- 様々なデータソースに対応
  - MySQL、PostgreSQL、MongoDB、BigQuery、Amazon Redshift、...
- シンプルで分かりやすく、簡単な操作でいい感じのグラフが作れる

---
layout: image
image: https://www.metabase.com/images/homepage-dashboard@2x.png
---

---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---

# Dockerで簡単に作成

jarファイル、Docker、SaaSの3つがある（SaaS版は有料）

<!-- $85/月なので個人向けではなさそう -->

```yaml
# docker-compose.yml
version: '3.8'

services:
  metabase:
    image: metabase/metabase:latest
    ports:
      - 3000:3000
```

デフォルトだとH2データベースが使われる（データがファイルに保存される）

---

# 作ったもの（製作中）

睡眠時間と歩数を可視化するもの（https://github.com/tekihei2317/personal-dashboard）

<img src="https://i.gyazo.com/f3877f2e246bef20be6a1bd9ec9058a5.png"/>

<style>
img {
  max-height: 80%;
}
</style>


---

# Metabaseで抑えておく概念は2つ

1つ目: 質問

- DBに問い合わせるクエリと、それを可視化したグラフのペア
- クエリはGUIで作成するか、エディターでSQLを直接書くことも出来る

<div class="grid grid-cols-2 gap-4" m="t-4">
  <div>GUI</div>
  <div>SQL</div>

  <img src="https://i.gyazo.com/ae0cee6864dfc4ee267c27331f05e425.png" class="h-full" />
  <img src="https://i.gyazo.com/e428ec5a1b1d3dab587cacdbea56531a.png" />
</div>

<style>
img {
  height: 280px;
}
</style>

---

# Metabaseで抑えておく概念は2つ

2つ目: ダッシュボード

- 作成した質問を配置する場所
- グラフの見た目を調整したり、テキストボックス（Markdown対応）を置ける

<!-- 見た目の調整 = 色、大きさなど -->
<!-- テキストボックスはMarkdown対応 -->
<!-- 質問を作る → ダッシュボードに置く、というように作っていく -->

<img src="https://i.gyazo.com/8b2c5b638db5b80dd82b3feba787d5dd.png" class="mt-4" />

<style>
img {
  max-height: 70%;
}
</style>

---

# これから

自動化 & 生産性の可視化

- 自動化
  - バッチでAPIからデータを取得できるようにする
- 生産性の可視化
  - GitHubのコントリビューション数（GitHub API）
  - GitHubの変更を加えた行数（GitHub API？）
  - 投稿した記事数
  - コーディング時間（WakaTime API）

...など

---

# WakaTime

エディタに拡張機能を入れると作業時間を計測してくれる

<div grid="~ cols-2 gap-4" m="t-4">
  <img src="https://i.gyazo.com/77b5a5e21ca425b3a6f0683ba908070b.png" />
  <img src="https://i.gyazo.com/b8d7b2878ed842036fa5dbc821b5cbb3.png" />
</div>

---

# 参考資料

- [OSSのデータ可視化ツール「Metabase」が超使いやすい - Qiita](https://qiita.com/acro5piano/items/0920550d297651b04387)