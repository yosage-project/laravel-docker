# 今日のおしながき

- Dockerの基本的な事項について
- docker run, docker composeの違いについて
- docker compose を使ったコンテナの作成の実演
  - Laravel(PHP8.2)
  - Nginx
  - MySQL

## Dockerの基本的なことについて

- コンテナと呼ばれる仮想開発環境を作成するためのツール
- 仮想マシンとコンテナの違いについて
  - コンテナはOSの上に箱を載せるイメージ
  - コンテナはOSの上に乗っているので、最終的な挙動はOSに依存します
    - 例えばLinuxで動かしていれば、LinuxのOSの制御外の動作はできません
    - Macで動かしていれば、MacのOSの制御外の動作はできません
  - 仮想マシンはOSそのもから全てをエミュレートします
    - OS, メモリ, HDD等々のサーバーを構成するすべての要素をを模倣します
    - なので仮想マシンの設定次第ではWindowsだろうが、Macだろうが、Linuxだろうが動かせます
    - 仮想マシン上にDockerを使ってコンテナを動作させることもできます
      - これのよくある例がAWS EC2上でコンテナを実行したりするなど
      - AWS ECSはEC2でコンテナを実行することでできてます
      - AWSのKebernetesも同様です
- コンテナで何ができるか
  - 特定の環境を模して、実行環境を用意することができる
    - 今回の場合だとPHP, MySQL, Nginxなどをエミュレートできます
  - 開発環境としてエンジニアに対して同一の環境を用意することができます
  - 同じDockerコンテナを使って本番環境の構築もできます


## docker run, docker composeの違いについて

### docker runは1つのコンテナを動かすためのコマンド

- docker pull: コンテナイメージを取得するコマンド
- docker create: イメージからコンテナを作成するコマンド
- docker start: 作成したコンテナを実行するコマンド

上の3つを同時に実行できるのがdocker runです。


### docker composeは複数のコンテナを同時に制御することができます

docker-compose.yamlもしくはcompose.yamlに記載しているコンテナ情報をもとに複数のコンテナを実行することができます。

docker runだと複数コンテナがある場合に複数回コマンドの実行が必要ですが、docker composeだと1回で済むので楽です。


## docker compose を使ったコンテナの作成の実演

最終的な目標はDockerを使ってPHPのフレームワークであるLaravelを実行し、ブラウザにウェルカムページを表示すること。

- Nginx
  - Webサーバーとして利用します
  - Apacheと並んでよく利用されるWebサーバーです
- PHP8.2
  - Laravelを実行するためのプログラミング言語
- MySQL
  - データベースとして利用します
  - PostgreSQL, Microsoft SQL Serverなども使わたりする