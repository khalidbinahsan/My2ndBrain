If your server uses Apache you can a add the following code on your **.htaccess** file
```php
RewriteEngine On
RewriteCond %{HTTP_HOST} ^printagraphy\.co\.uk [NC,OR]
RewriteCond %{HTTP_HOST} ^www\.printagraphy\.co\.uk [NC]
RewriteRule ^(.*)$ https://printagraphy.com/$1 [L,R=301]
```