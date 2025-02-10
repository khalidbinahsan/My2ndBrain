Add this following code to `functions.php`
```php
add_filter('woocommerce_order_button_text', function() {
    return 'Purchase Now';
});
```