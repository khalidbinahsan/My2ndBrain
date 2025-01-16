Look at the following command to integrate Laravel with Vue.js through Inertia
## 1. Install Laravel
```bash
composer create-project laravel/laravel my-project
cd my-project
```
## 2. Install Inertia.js
```bash
composer require inertiajs/inertia-laravel
```
Next, create the Inertia middleware
```bash
php artisan inertia:middleware
```
## 3. Install Vue.js and the Inertia Client
```bash
npm install vue @vitejs/plugin-vue @inertiajs/vue3
```
## 4. Configure Vite for Vue.js
Update your `vite.config.js` file to enable Vue.js support
```js
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/js/app.js', 'resources/css/app.css'],
            refresh: true,
        }),
        vue(),
    ],
});
```
## 5. Setup the Inertia App
Modify your `resources/js/app.js` file fo initialize Vue and Inertia
```js
import { createApp, h } from 'vue';
import { createInertiaApp } from '@inertiajs/vue3';
import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';
import '../css/app.css';

createInertiaApp({
    resolve: (name) => resolvePageComponent(`./Pages/${name}.vue`, import.meta.glob('./Pages/**/*.vue')),
    setup({ el, App, props, plugin }) {
        createApp({ render: () => h(App, props) })
            .use(plugin)
            .mount(el);
    },
});
```
## 6. Create an Inertia Root View
Update your `resources/views/app.blade.php` file
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    @vite(['resources/js/app.js', 'resources/css/app.css'])
    @inertiaHead
</head>
<body>
    @inertia
</body>
</html>
```
## 7. Add Middleware
Update the middleware on `bootstrap/app.php` file
```php
use App\Http\Middleware\HandleInertiaRequests;

 ->withMiddleware(function (Middleware $middleware) {
        $middleware->web(append: [
            HandleInertiaRequests::class,
        ]);
    })
```
## 8. Create a Vue Page Component
Create your first Vue component in the `resources/js/Pages.vue` directory. For example, `resources/js/Pages/Home.vue`
```vue
<script setup>

</script>

<template>
<h1 class="text-3xl">Welcome to the Vue Inertia</h1>
</template>

<style scoped>

</style>
```
## 9. Create a Route and Controller
Define a route in `routes/web.php` that returns an inertia response
```php
<?php

use Inertia\Inertia;
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return Inertia::render('Home');
});
```
## 10. Compile Assets and Serve
```bash
npm run dev
php artisan serve
```