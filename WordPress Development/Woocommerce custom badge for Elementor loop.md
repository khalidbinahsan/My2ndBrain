```php
add_shortcode('custom_product_badges', 'custom_woocommerce_product_badges');
function custom_woocommerce_product_badges() {
    global $product;

    // Initialize badge output
    $badge_output = '';

    // New Badge: Check if the product was published in the last 30 days
    $new_days = 30;
    $post_date = strtotime($product->get_date_created());
    $current_date = strtotime(current_time('Y-m-d H:i:s'));
    if (($current_date - $post_date) / (60 * 60 * 24) <= $new_days) {
        $badge_output .= '<span class="custom-badge new"><img src="/wp-content/uploads/2025/01/new-1.png"></span>';
    }
    // Sale Badge: Check if the product is on sale
    if ($product->is_on_sale()) {
        $badge_output .= '<span class="custom-badge sale"><img src="/wp-content/uploads/2025/01/sale-1.png"></span>';
    }

    return $badge_output;
}

```