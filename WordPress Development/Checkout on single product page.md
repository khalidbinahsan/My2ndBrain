First of all place your checkout form any where and modify it as you want. Then add this code to your functions.php
```php
add_action('wp', function() {
    if (is_product() && !is_admin() && WC()->cart) {
        $product_id = get_queried_object_id(); // Get the current product ID

        // Ensure we have a valid product ID
        if (!$product_id) {
            return;
        }

        // Clear the cart before adding a new product
        WC()->cart->empty_cart();

        // Add the new product to the cart
        WC()->cart->add_to_cart($product_id);
    }
});
```