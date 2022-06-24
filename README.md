# 起動・再起動・全削除
docker-compose up -d
docker-compose restart
docker-compose down --rmi all --volumes --remove-orphans

# laravelインストール
composer create-project --prefer-dist laravel/laravel . "9.*"
chmod -R 777 storage
chmod -R 777 bootstrap/cache/

# migration ＋ model ⇒ php artisan make:model Models/【単数モデル名】 --migration
php artisan make:model Models/Cart --migration

# migration 既存テーブルにカラム追加 artisan make:migration add_【カラム名】_column_to_【テーブル名】_table --table=【テーブル名】
php artisan make:migration add_postal_column_to_orders_table --table=orders

# migration やり直し ＋ SEED
php artisan migrate:refresh --seed
php artisan migrate:fresh --seed

# ミドルウェア作成 ⇒ php artisan make:middleware 【ミドルウェア名】
php artisan make:middleware CartSession

# seeder 作成 artisan make:seeder 【シーダ名】
php artisan make:seeder DatabaseSeeder

# seeder 実行 artisan db:seed --class= 【シーダ名】
php artisan db:seed --class=DatabaseSeeder

# seeder 実行不可の場合（Class hogeSeeder does not exist.）
composer dump-autoload
php artisan db:seed --class=DatabaseSeeder

# component 作成
php artisan make:component Header

# PHPの実行
php artisan tinker
例：ItemCondition::orderBy('sort_no')->toSql()

# 所有権者変更
chown -R 1000:1000 database/seeders/*

# キャッシュクリア
php artisan cache:clear &&
php artisan config:clear &&
php artisan config:cache &&
php artisan route:clear &&
php artisan view:clear &&
php artisan clear-compiled &&
php artisan optimize &&
composer dump-autoload &&
rm -f bootstrap/cache/config.php

# node + npm インストール
apt update
apt install -y nodejs npm
npm install n -g
n lts
apt purge nodejs npm
docker exec 〜 (再ログイン)
node -v
npm -v
npm install

# npm 再インストール
npm cache clean -f
rm -rf node_modules
npm install