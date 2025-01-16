Add this to your function.php and add the shortcode to the Elementor loop item
```php
function custom_cart_icon_shortcode($atts) {
    global $product;
    // Default to the current product if no product_id is provided
    $atts = shortcode_atts(array(
        'product_id' => $product ? $product->get_id() : null,
    ), $atts);
    $product_id = intval($atts['product_id']);
    $product = wc_get_product($product_id);
    if (!$product || !$product->is_purchasable() || !$product->is_in_stock()) {
        return ''; // Return nothing if the product is not purchasable or out of stock
    }
    // Generate the Add to Cart link
    $add_to_cart_url = esc_url($product->add_to_cart_url());
    $add_to_cart_text = esc_attr($product->add_to_cart_text());
    return sprintf(
        '<a href="%s" data-quantity="1" data-product_id="%d" class="button product_type_simple add_to_cart_button ajax_add_to_cart" aria-label="%s">
            <i class="fas fa-shopping-cart"></i>
        </a>',
        $add_to_cart_url,
        $product_id,
        $add_to_cart_text
    );
}
add_shortcode('cart_icon', 'custom_cart_icon_shortcode');
```