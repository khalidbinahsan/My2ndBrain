You can use this PHP function in your theme file (e.g., `header.php`, `page.php`, or via a shortcode)
```php
if (function_exists('woocommerce_breadcrumb')) {
    woocommerce_breadcrumb();
}
```
If you want to use it in Elementor or a page editor with a shortcode like `[woocommerce_breadcrumb]`, add this to your theme’s `functions.php`:
```php
function custom_woocommerce_breadcrumb_shortcode() {
    ob_start();

    if (function_exists('woocommerce_breadcrumb')) {
        woocommerce_breadcrumb();
    }

    return ob_get_clean();
}
add_shortcode('woocommerce_breadcrumb', 'custom_woocommerce_breadcrumb_shortcode');
```
You can customize WooCommerce breadcrumb settings like delimiter, wrapper, etc., by passing arguments to `woocommerce_breadcrumb()`
```php
woocommerce_breadcrumb( array(
    'delimiter'   => ' &raquo; ',
    'wrap_before' => '<nav class="woocommerce-breadcrumb">',
    'wrap_after'  => '</nav>',
) );
```
