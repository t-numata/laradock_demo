# laradock_demo
## 概要

LaravelをLaradock上で動かすためのデモです。
あくまでデモ用なので、プロダクトなどには用いないでください。

### デフォルトの環境

このページの手順に従って進めると、以下の環境が起動します。
その他構成を試す場合はLaravel/Laradockのドキュメントを参考にしてください。

* webサーバ
	* nginx
* DB
	* postgres
		* db name: laradock_demo
		* db password: secret
		* db username: default
* cache
	* redis

## demo環境構築手順
1. このリポジトリをgit clone
2. /laradock_demoの階層まで移動
3. sh setup.shを実行
4. laradock_demoの階層へ移動
5. dockerコンテナの起動
``` sh
# laradock_demo/
docker-compose up -d nginx postgres redis
```
6. workspaceへアクセス
``` sh
# laradock_demo/
docker-compose exec workspace bash
```
7. composer install
``` sh
# in workspace container
composer install
```

8. DBのマイグレーションを実行
``` sh
# in workspace container
php artisan migrate
```
9. localhostにアクセス

10. コンテナの停止
``` sh
# laradock_demo/
php artisan migrate
```
## 各コンテナの情報
### workspace
### アクセス方法
``` sh
# laradock_demo/
docker-compose exec workspace bash
```
	
#### 機能
* laradockが自動的に立ち上げるコンテナ
* laravelのCLIコマンドや、composer命令の発行などはこのコンテナで行う

### php-fpm
#### アクセス方法
``` sh
# laradock_demo/
docker-compose exec php-fpm bash
```
#### 機能
* laradockが自動的に立ち上げるコンテナ
* その名の通り  nginx用のphp-fpm

### postgres
#### アクセス方法
``` sh
# laradock_demo/
docker-compose exec postgres bash
# ココから postgresコンテナ内
su - postgres
```
#### 機能
* laravelからアクセスするDB用コンテナ
	* 今回はpostgresで用意していますが、laradockでは他のDBも使用可能です
	* 詳細はlaradockドキュメントを確認してください。
	
###  redis
#### アクセス方法

``` sh
# laradock_demo/
docker-compose exec redis bash
# ココから redisコンテナ内
redis-cli
```

#### 機能
* redis用のコンテナ

### nginx
#### アクセス方法

``` sh
# laradock_demo/
docker-compose exec nginx bash
```
#### nginxログ標準出力方法
``` sh
# laradock_demo/
docker-compose logs -f nginx
```
#### 機能
* nginx用のコンテナ


#work/opensmile
