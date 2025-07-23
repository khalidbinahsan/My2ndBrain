Add the code in your `wp-config.php`
```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false); // So it doesn't show on the frontend
```
check the file in `wp-content/debug.log`