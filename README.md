# self_dockermachine

## これはなに？

dockerのサーバーを構築するVagrantfileです。

`vagrant up`を実行すると構築されます。
ホスト側で`docker -H tcp://127.0.0.1:12375 {なにかコマンド}`と実行すると、
サーバーに接続して処理がされます。

## 必要なもの

Vagrant
Virtualbox
docker

## 実行ためした環境

mac
Vagrant
VirtualBox
docker for mac


## どんなときにつかえる？

docker for mac/docker for windowsよりもより詳細に
サーバー側の設定をしたいときに使えるかも。
そもそもそんなケースはあまりないかもしれないが。


## 参考にしたもの

https://docs.docker.com/engine/install/linux-postinstall/#configuring-remote-access-with-systemd-unit-file

dockerはデフォルトではunixソケット通信しか許可していないのですが、
tcp通信をするときはdocker daemonのオプションを指定すれば良いことがわかりました。

Vagrant + VirtualBoxで仮想環境側のポートをあける
https://qiita.com/kkam0907/items/4a345cd5e834969d3859

ゲストマシン内では`telnet localhost 2375`でつながるのにホストマシンからは接続できないってなったとき、参考になりました。ファイアウォールが邪魔していた。


##　その他

めんどくさがってtlsで通信するのはオフにしています。
ローカルでしか使わないから大丈夫だろうという雑な感じで。