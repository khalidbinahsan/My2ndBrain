If you want to redirect to checkout page when you add to cart any product. Here is the simple code add to your **functions.php** file.
```php
add_filter('woocommerce_add_to_cart_redirect', 'redirect_to_checkout');
function redirect_to_checkout() {
    return wc_get_checkout_url();
}
```