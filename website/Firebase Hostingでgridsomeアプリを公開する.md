# Firebase Hostingでgridsomeアプリを公開する

## 手順

### Firebase CLIのインストール

```text
npm install -g firebase-tools
```

### Firebase CLIの認可

```text
$ firebase login
# ブラウザが開かれるので、Firebase CLIからのリソースの操作を許可する
```

### デプロイ用の設定ファイルの作成

使用するFirebaseの機能は`Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys`を選択した。

公開するディレクトリ、ビルド時のコマンド、GitHub Actionsの設定等が出てくるのでよしなに入力していく。

### デプロイ

```text
$ firebase deploy
# 表示されたURLを開くとホスティングされたサイトが確認できた
```

## 生成されたGitHub Actionsのワークフローファイルを見てみる

```yaml
# firebase-hosting-merge.yml
name: Deploy to Firebase Hosting on merge
'on':
  push:
    branches:
      - main
jobs:
  build_and_deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: yarn build
      - uses: FirebaseExtended/action-hosting-deploy@v0
        with:
          repoToken: '${{ secrets.GITHUB_TOKEN }}'
          firebaseServiceAccount: '${{ secrets.FIREBASE_SERVICE_ACCOUNT_HIFU_HP }}'
          channelId: live
          projectId: hifu-hp
```

`main`ブランチに変更が加わったときにデプロイしている。
TODO: `secrets.GITHUB_TOKEN`について調べる。`secrets.FIREBASE_SERVICE_ACCOUNT_xxx`についてはリポジトリのsecretsに保存されていた。

```yaml
# firebase-hosting-pull-request.yml
name: Deploy to Firebase Hosting on PR
'on': pull_request
jobs:
  build_and_preview:
    if: '${{ github.event.pull_request.head.repo.full_name == github.repository }}'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: yarn build
      - uses: FirebaseExtended/action-hosting-deploy@v0
        with:
          repoToken: '${{ secrets.GITHUB_TOKEN }}'
          firebaseServiceAccount: '${{ secrets.FIREBASE_SERVICE_ACCOUNT_HIFU_HP }}'
          projectId: hifu-hp
```

`main`へのPRに変更が加わったときに、プレビュー用のデプロイをしている？

ワークフローファイルに`yarn install`を書き忘れていたので追記した。yarnのパッケージをキャッシュしていないので少し時間がかかるが、大体2分くらいでデプロイが完了した。

## 参考

- [Firebase Hosting](https://firebase.google.com/docs/hosting/?authuser=0#implementation_path)
- [Firebase公式のGitHubとHostingのインテグレーションが熱い🔥](https://zenn.dev/watarukun/articles/8f3e318bacf97cabf879)
- [WordPressで記事を投稿したらGitHub Actions経由でGridsomeのビルドをする。 - return $lock;](https://retrorocket.biz/archives/1606)
- [GitHubActionsのrepository_dispatchを使い特定ブランチでWorkflowを実行する - notebook](https://swfz.hatenablog.com/entry/2020/01/23/080000)
