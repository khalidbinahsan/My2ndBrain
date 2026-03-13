```php
// Include SKU in Elementor and WordPress search
function include_product_sku_in_search( $query ) {
    if ( ! is_admin() && $query->is_main_query() && $query->is_search() ) {
        $search_term = $query->get( 's' );

        // Find products with matching SKU
        $sku_query = new WP_Query( array(
            'post_type'      => 'product',
            'posts_per_page' => -1,
            'meta_query'     => array(
                array(
                    'key'     => '_sku',
                    'value'   => $search_term,
                    'compare' => 'LIKE'
                ),
            ),
            'fields' => 'ids'
        ) );

        $sku_ids = $sku_query->posts;

        // Merge with normal search results
        if ( ! empty( $sku_ids ) ) {
            $query->set( 'post_type', array( 'product' ) );
            $query->set( 'post__in', $sku_ids );
            $query->set( 's', '' ); // disable default title/content search if SKU found
        }
    }
}
add_action( 'pre_get_posts', 'include_product_sku_in_search' );

```