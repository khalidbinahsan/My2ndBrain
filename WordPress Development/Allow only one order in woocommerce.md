Add the following code to the `functions.php`
```php
function sitename_allow_only_one_in_cart($passed) {
  wc_empty_cart();
  return $passed;
}
add_filter('woocommerce_add_to_cart_validation', 'sitename_allow_only_one_in_cart', 9999);
```