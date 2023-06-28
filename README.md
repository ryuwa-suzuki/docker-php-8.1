# docker-php-8.1
php8.1-apache, mailcatcher, phpmyadmin

# Readme


## 環境

- php:8.1.0

- mysql 8.0

## 前提条件
- dockerがインストールされていること

## 構築手順

### 1.  .envファイルを作成し、プロジェクト名を書き込む
```
# git cloneしたディレクトリ上で実行
$ cp env.example .env
```
複製された.envファイルを開き任意のプロジェクト名を書き込む
```
COMPOSE_PROJECT_NAME={プロジェクト名}
```

### 2. Git
- www配下にgit cloneしたプロジェクトのディレクトリをhtmlフォルダとして配置
 ```
 # git cloneしたディレクトリ上で実行
 $ cd www
 $ git clone {リポジトリパス} html
  ```


### 3. DocumentRootの設定
- docker/app/000-default.confファイルを開き、12行目と14行目を編集
```
# 12行目
DocumentRoot /var/www/html/public
↓
DocumentRoot /var/www/html/{ドキュメントルート}
# 14行目
<Directory /var/www/html/public>
↓
<Directory /var/www/html/{ドキュメントルート}>
```
※laravelの場合は/var/www/html/public

### 4. Dockerビルド・起動

- ビルド
```
$ docker-compose build
```
- 起動
```
$ docker-compose up

```

※ コンテナ停止・削除
```
# 停止
$ docker-compose stop
# 削除
$ docker-compose down
```


## 確認

### web

* http://localhost


### MailCatcher

* http://localhost:1080/


### phpMyAdmin

* http://localhost:8080/


### コンテナにログイン

```
// 任意のディレクトリ
$ docker exec -it {envに登録したプロジェクト名}_web_1 bash
```