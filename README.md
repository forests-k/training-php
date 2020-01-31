# PHP/Laravel training

## 開発環境
- Window10
- Docker Desktop for Windows
- Git

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

TBA
```terminal
>docker -v
Docker version 19.03.5, build 633a0ea
```
  
1. [Docker Compose](http://docs.docker.jp/compose/overview.html)コマンドを利用して、コンテナを起動
  
```terminal
>cd {project repository}
> docker-compose up -d
```