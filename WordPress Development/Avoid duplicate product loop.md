Add this code to `functions.php`
```php
add_action('woocommerce_product_query', function($query) {
    if (is_front_page()) {
        $popular_ids = get_posts([
            'post_type'      => 'product',
            'posts_per_page' => 6, // Adjust to match the number of popular products displayed
            'orderby'        => 'popularity',
            'fields'         => 'ids', // Get only IDs
        ]);

        if (!empty($popular_ids)) {
            $query->set('post__not_in', $popular_ids);
        }
    }
});

```