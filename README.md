# docker

Dockerを使用した開発用サーバーの構築

## 概要

自分用の開発サーバーが欲しくて、Raspberry PiにDockerを使用してサーバーを構築しました。

> [!CAUTION]
>
> あくまで簡易的なのでセキュリティが考慮されていません。
>
> 外部からアクセスされないLAN内での使用を想定しています。

## 使用環境

- Raspberry Pi 3B+

- Raspberry Pi OS Lite

  - System 64bit

  - Kernel version 6.18

## 前提

ユーザーID:1000、グループID:1000のユーザーで実行することを前提としています。

## インストール

1. Dockerをインストールします。

   ```bash
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh ./get-docker.sh --dry-run
   ```

1. ユーザーをdockerグループに追加します。

   ```bash
   sudo usermod -aG docker $USER
   ```

1. このリポジトリをホームディレクトリにクローンします。

   ```bash
   git clone https://github.com/wishbird160/docker.git
   ```

1. dockerディレクトリに移動して、Dockerコンテナを作成・構築・起動します。

   ```bash
   cd docker
   docker compose up -d
   ```

## サーバーの構成

| サーバーの種類 | ポート        | 説明                                                                                                 |
| -------------- |:-------------:| ---------------------------------------------------------------------------------------------------- |
| Wiki.js        | 80            | 最初に登録するユーザーは管理者になります。                                                           |
| Redmine        | 3000          | 初期ユーザー: admin<br/>初期パスワード: admin                                                        |
| GitBucket      | 8080          | 初期ユーザ: root<br/>初期パスワード: root                                                            |
| FileBrowser    | 5000          | 初期ユーザ: admin<br/>初期パスワード:自動生成されます。<br/>`docker compose logs file`で確認します。 |
| Mailpit        | 1025<br/>8025 | 1025はSMTPのポート番号です。<br/>8025はWebメールのポート番号です。                                   |

## サーバーの停止方法

dockerディレクトリの中でコマンドを実行します。

```bash
docker compose down
```

## サーバーのデータをリセットする方法

1. サーバーを停止してから、dockerディレクトリの中でコマンドを実行します。

```bash
docker compose down
docker volume prune -a
rm -rf $HOME/docker/filebrowser/folder/*
```
