## Introduction

[Laravel Telescope](https://github.com/laravel/telescope) makes a wonderful companion to your local Laravel development environment. Telescope provides insight into the requests coming into your application, exceptions, log entries, database queries, queued jobs, mail, notifications, cache operations, scheduled tasks, variable dumps, and more.
## Installation
You may use the Composer package manager to install Telescope into your Laravel project:
```bash
composer require laravel/telescope
```
After installing Telescope, publish its assets and migrations using the `telescope:install` Artisan command. After installing Telescope, you should also run the `migrate` command in order to create the tables needed to store Telescope's data:
```bash
php artisan telescope:install

php artisan migrate
```
Now you can access it from the route ==/telescope==
