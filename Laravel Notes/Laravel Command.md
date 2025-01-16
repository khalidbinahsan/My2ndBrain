## api.php
By default in Laravel 11, the api.php is not included in routes folder. To create that write the following command
```bash
php artisan install:api
```
## Seeder
Seeder is to create the demo data in database
### Create seeder
```bash
php artisan make:seeder SeederName
```
### Run the seeder
```bash
php artisan db:seed --class=SeederName
```
### Run all seeder
```bash
php artisan db:seed
```
### Run Seeders with Migrations
```bash
php artisan migrate --seed
```