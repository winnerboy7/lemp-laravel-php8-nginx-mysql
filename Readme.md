https://www.digitalocean.com/community/tutorials/how-to-set-up-laravel-nginx-and-mysql-with-docker-compose

# Step 1 — Downloading Laravel and Installing Dependencies
cd ~
git clone https://github.com/laravel/laravel.git laravel-app

cd ~/laravel-app

docker run --rm -v $(pwd):/app composer install

sudo chown -R sammy:sammy ~/laravel-app

# Step 2 — Creating the Docker Compose File
nano ~/laravel-app/docker-compose.yml


# Step 3 — Persisting Data


# Step 4 — Creating the Dockerfile

nano ~/laravel-app/Dockerfile

# Step 5 — Configuring PHP

mkdir ~/laravel-app/php
nano ~/laravel-app/php/local.ini

php/local.ini
upload_max_filesize=40M
post_max_size=40M

# Step 6 — Configuring Nginx

mkdir -p ~/laravel-app/nginx/conf.d
nano ~/laravel-app/nginx/conf.d/app.conf


# Step 7 — Configuring MySQL

mkdir ~/laravel-app/mysql
nano ~/laravel-app/mysql/my.cnf

# Step 8 — Modifying Environment Settings and Running the Containers

cp .env.example .env
nano .env

docker-compose up -d
docker ps
docker-compose exec app php artisan key:generate
docker-compose exec app php artisan config:cache


# Step 9 — Creating a User for MySQL

docker-compose exec db bash

mysql -u root -p
show databases;
GRANT ALL ON laravel.* TO 'laraveluser'@'%' IDENTIFIED BY 'your_laravel_db_password';
FLUSH PRIVILEGES;
EXIT;
exit


# Step 10 — Migrating Data and Working with the Tinker Console

docker-compose exec app php artisan migrate
docker-compose exec app php artisan tinker
\DB::table('migrations')->get();

