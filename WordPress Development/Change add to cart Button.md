If you want to change the **Add to cart Button** text, here is the simple code add to your **functions.php** file
```php
add_filter( 'woocommerce_product_single_add_to_cart_text', 'woocommerce_custom_single_add_to_cart_text' ); 
function woocommerce_custom_single_add_to_cart_text() {
    return __( 'Your button text here', 'woocommerce' ); 
}
```