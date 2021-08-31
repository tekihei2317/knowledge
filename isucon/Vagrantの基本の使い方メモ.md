# Vagrantの基本の使い方メモ

## 基本のコマンド

```bash
# 仮想マシンの起動(1回目は時間がかかる、2回目以降は早い)
vagrant up

# 仮想マシンに接続
vagrant ssh

# 仮想マシンの状態を確認
vagrant status

# 仮想マシンを停止
vagrant stop

# 再構築（環境を壊した場合に1から作り直す?）
vagrant provisioon

# 停止 & 破壊 & 再作成
vagrant halt && vagrant destroy -f && vagrant up

# ?
vagrant reload
```

## VSCodeのRemote SSHで仮想マシンに接続する

`vagrant ssh-config`で接続設定が出力されるので、それを`~/.ssh/config`に追記すれば良い。

```bash
vagrant ssh-config >> ~/.ssh/config
```

## 参考

- [VagrantでVScodeのRemote Developmentを使おう！ - Qiita](https://qiita.com/hppRC/items/9a46fdb4af792a454921)
- [Vagrant Provisionとは - Qiita](https://qiita.com/wakky_404/items/710f08c865969e72df73)
  - `vagrant provision`についてはこれを読む
- [Vagrantで仮想マシンを停止＆破壊＆再作成するワンライナー - Qiita](https://qiita.com/DQNEO/items/5ee05ce7afb8fc9c6656)
