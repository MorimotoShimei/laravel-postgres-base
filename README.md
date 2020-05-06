
# Laravel + vue + Postgres (base)

## 構築

docker-composeを起動

```sh
docker-compose up -d
```

コンテナ内に入る

```sh
docker-compose exec web bash
```

Laravel プロジェクトを作成

```sh
# コンテナ内で実行
composer create-project --prefer-dist laravel/laravel .
composer require laravel/ui
chmod 770 -R storage/
chmod 770 -R bootstrap/cache/
npm install
npm install -D vue vuex vue-router
```

.envを編集

APP_URL、DB_CONNECTION、DB_HOST、DB_PORT、DB_DATABASE、DB_USERNAME、DB_PASSWORD

```sh
APP_URL=http://localhost:8080

DB_CONNECTION=pgsql
DB_HOST=web_db
DB_PORT=5432
DB_DATABASE=postgres
DB_USERNAME=postgres
DB_PASSWORD=secret
```

サーバを起こす

```sh
# コンテナ内で実行
php artisan serve --host 0.0.0.0 --port 8080
```

## 実行

envをコピー

```sh
cp web/.env.example web/.env
```

docker-composeを起動

```sh
docker-compose up -d
```

コンテナ内に入る

```sh
docker-compose exec web bash
```

モジュールのインストール、DBにテーブルを構築

```sh
# コンテナ内で実行
chmod 770 -R storage/
chmod 770 -R bootstrap/cache/
composer install
npm install
npm run dev
php artisan migrate
```

サーバを起こす

```sh
# コンテナ内で実行
php artisan serve --host 0.0.0.0 --port 8080
```

### 参考：ホストから実行する場合

```sh
docker-compose exec web php artisan serve --host 0.0.0.0 --port 8080
```

npmをホスト側から実行する場合

```sh
docker-compose exec web npm install
docker-compose exec web npm run watch
```

テスト docker内で実行

```sh
vendor/bin/phpunit --testdox
```
