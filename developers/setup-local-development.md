# Setup local development

These are the steps required to setup the local development.

Monica is a Laravel application. That means it requires this setup:

* PHP 8.1 or newer
* HTTP server with PHP support (eg: Apache, Nginx, Caddy)
* Composer
* MySQL

You can find more details on the Laravel documentation website.

1. Install PHP and a web server like Nginx. If you are on macOS, we recommend [Valet](https://laravel.com/docs/9.x/valet)
2. Install [SQLite](https://formulae.brew.sh/formula/sqlite) or MySQL
3. `composer install --no-progress --no-interaction --prefer-dist --optimize-autoloader`
4. `yarn install --frozen-lockfile`
5. `cp .env.example .env` and configure `.env` file
   1. `php artisan key:generate --no-interaction` (generates APP\_KEY)
   2. `touch monica.db` (if you use SQLite) and add the path to DB\_DATABASE
6. `php artisan monica:setup --force -vvv`
7. Optional: generate dummy data
   1. `php artisan monica:dummy --force -vvv`
8. Optional: make the search work:
   1. Install and run [meilisearch](https://www.meilisearch.com/) locally
   2. Configure and run a queue (`php artisan queue:listen --queue=high,low,default`)
9. `yarn build` to generate the proper JS and CSS files
10. `yarn dev` and head to your browser to play with Monica
