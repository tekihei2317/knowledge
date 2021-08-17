# 最近の開発環境の改善: VSCode編(2021年8月)

## Markdown Preview Enhancedを導入

**before**

<img src="https://i.gyazo.com/8088fa05cb17614fe3a1c0d0284fede0.png" style="width: 70%">

**after**

<img src="https://i.gyazo.com/c47dfbb41af68f045d751a2e7ce4b323.png" style="width: 70%">

- Markdownを書くのが楽しくなった。最高。

## Project Manajerからpeco+ghqに移行

- pecoとghqを使って、gitリポジトリをVSCodeで開く操作をターミナルから行えるようにした
  - pcodeがVSCodeで開く関数で、prepoがリポジトリに移動する関数
  - 現状はEnterを2回押さないといけないので若干改善の余地あり

```bash
# ~/.zshrc
function pcode () {
  local repo=$(ghq list | peco --query "$LBUFFER")
  if [ -n "$repo" ]; then
    repo=$(ghq list --full-path --exact $repo)
    print -z "code ${repo}"
  fi
}

function prepo () {
  local repo=$(ghq list | peco --query "$LBUFFER")
  if [ -n "$repo" ]; then
    repo=$(ghq list --full-path --exact $repo)
    print -z "cd ${repo}"
  fi
}
```

- マウスやタッチパッドでの不安定な操作を、キーボードで出来るようにすると効率化につながると感じた

## タブを閉じたときの挙動を変更

- Chromeみたいにタブを右から順番に閉じれるようにした
  - setting.jsonに以下を追記
  - デフォルトの挙動は閉じた後どこに移動するか予測出来なかったので少し気になっていた
```json
{
  "workbench.editor.focusRecentEditorAfterClose": false
}
```

## 参考

- [ghq handbook Masayuki Matsuki (Songmu) 著 [Leanpub PDF/iPad/Kindle]](https://leanpub.com/ghq-handbook)
- [これこそ一番望んでいた機能かも？ Visual Studio Code 1.31 リリースまとめ！ | 株式会社ビヨンド](https://beyondjapan.com/blog/2019/02/vscode-131/)
