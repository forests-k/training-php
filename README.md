# PHP/Laravel training

## 開発環境
- Window10
- Docker Desktop for Windows
- Git
- curl

## 環境構成
- PHP 7.4
- Laravel 6.2
- MySQL 8
- Nginx 1.17.8

## 参考資料
- [【Docker Compose】設定内容を1行ずつ理解しながらLaravel環境構築（PHP-FPM、Nginx、MySQL、Redis） - Qiita](https://qiita.com/minato-naka/items/8b31d28823cabaa9487a)
- [Docker Hub](https://hub.docker.com/)
- [Docker Compose 概要 — Docker-docs-ja 17.06.Beta ドキュメント](http://docs.docker.jp/compose/overview.html)
- [GitHub - php/php-src at PHP-7.4.0](https://github.com/php/php-src/tree/PHP-7.4.0)
- [PHP: PHP マニュアル - Manual](https://www.php.net/manual/ja/)
- [Laravel - ウェブ職人のためのPHPフレームワーク](http://laravel.jp/)

## 開発環境構築
1. [docker hub](https://hub.docker.com/)でアカウント作成
2.  [docker hub](https://hub.docker.com/)から[Docker Desktop for Windows](https://hub.docker.com/)をダウンロード、インストール
3.  コマンドでDocker Desktop for Windowsが有効となっていることを確認

```terminal
>docker -v
Docker version 19.03.5, build 633a0ea
```
4. GitHubからプロジェクトを任意のリポジトリにクローン

対象のリポジトリは、[GitHub - forests-k/training-php](https://github.com/forests-k/training-php)から参照
```terminal
>git clone https://github.com/forests-k/training-php.git
Cloning into 'training-php'...
remote: Enumerating objects: 17, done.
remote: Counting objects: 100% (17/17), done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 17 (delta 0), reused 17 (delta 0), pack-reused 0
Unpacking objects: 100% (17/17), done.
```
  
  5. [Docker Compose](http://docs.docker.jp/compose/overview.html)コマンドを利用して、コンテナを起動
  
```terminal
>cd {project repository}
>docker-compose up -d
Building proxy
Step 1/4 : FROM nginx:1.17.8
 ---> 5ad3bd0e67a9
Step 2/4 : ADD ./server.conf /etc/nginx/conf.d/default.conf
 ---> Using cache
 ---> 28f71cb28a98
Step 3/4 : WORKDIR /var/www
 ---> Using cache
 ---> 5381614cc327
Step 4/4 : RUN apt-get update &&     apt-get install -y vim &&     apt-get install -y curl
 ---> Running in 0df9093a9449

省略

Removing intermediate container 0df9093a9449
 ---> caf465051aeb

Successfully built caf465051aeb
Successfully tagged training-php_proxy:latest
WARNING: Image for service proxy was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Building db
Step 1/5 : FROM mysql:8.0
 ---> d0b76af27c77
Step 2/5 : RUN mkdir -p /var/log/mysql
 ---> Running in 9986fc8a5691
Removing intermediate container 9986fc8a5691
 ---> b0b5a95d87c0
Step 3/5 : RUN touch /var/log/mysql/mysqld.log
 ---> Running in 1033fd83c7d1
Removing intermediate container 1033fd83c7d1
 ---> c922d2dc1aa6
Step 4/5 : ADD ./conf.d/my.cnf /etc/mysql/conf.d
 ---> 22ac40181ab9
Step 5/5 : RUN chmod 644 /etc/mysql/conf.d/my.cnf
 ---> Running in 58d7d8522077
Removing intermediate container 58d7d8522077
 ---> a364116c5c58

Successfully built a364116c5c58
Successfully tagged training-php_db:latest
WARNING: Image for service db was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Building php
Step 1/5 : FROM php:7.4-fpm
 ---> 71f166899e8c
Step 2/5 : RUN docker-php-ext-install pdo_mysql
 ---> Using cache
 ---> 2682c04332fe
Step 3/5 : RUN curl -sS https://getcomposer.org/installer | php
 ---> Using cache
 ---> c43a4506b8e5
Step 4/5 : RUN mv composer.phar /usr/local/bin/composer
 ---> Using cache
 ---> 395f230cac8e
Step 5/5 : RUN apt-get update &&     apt-get install -y git
 ---> Using cache
 ---> ee346491d8fb

Successfully built ee346491d8fb
Successfully tagged training-php_php:latest
WARNING: Image for service php was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating laravel-training-db    ... done
Creating training-php-fpm       ... done
Creating laravel-training-proxy ... done
```

6. dokcer-composeコマンドで起動したコンテナを確認する

すべてのコンテナが起動(status = Up)であることを確認する
```terminal
>docker-compose ps
         Name                       Command              State                 Ports
---------------------------------------------------------------------------------------------------
laravel-training-db      docker-entrypoint.sh mysqld     Up      0.0.0.0:13306->3306/tcp, 33060/tcp
laravel-training-proxy   nginx -g daemon off;            Up      0.0.0.0:81->80/tcp
training-php-fpm         docker-php-entrypoint php-fpm   Up      0.0.0.0:9000->9000/tcp
```

7. 作成したコンテナtraining-php-fpmにログインし、PHPが起動するか確認する

123456789が出力されることを確認する
```terminal
>docker-compose run php /bin/bash
root@589c4eb21160:/var/www/html# php index.php
123456789
```
8. クライアントから、リバースプロキシであるNginxを経由してPHPのコンテナにアクセスできるか確認する

レスポンスの値が123456789であることを確認する
※ブラウザから出の確認でも可能
```terminal
>curl http://127.0.0.1
123456789
```
