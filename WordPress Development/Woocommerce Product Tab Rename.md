Add this code on your theme **functions.php** file
```php
// Rename WooCommerce product tabs
add_filter( 'woocommerce_product_tabs', 'rename_woocommerce_product_tabs', 98 );
function rename_woocommerce_product_tabs( $tabs ) {
    // Rename the description tab
    if ( isset( $tabs['description']['title'] ) ) {
        $tabs['description']['title'] = __( 'More Information', 'text-domain' ); // Change 'More Information' to your desired title
    }

    // Rename the additional information tab
    if ( isset( $tabs['additional_information']['title'] ) ) {
        $tabs['additional_information']['title'] = __( 'Product Details', 'text-domain' ); // Change 'Product Details' to your desired title
    }

    // Rename the reviews tab
    if ( isset( $tabs['reviews']['title'] ) ) {
        $tabs['reviews']['title'] = __( 'Customer Reviews', 'text-domain' ); // Change 'Customer Reviews' to your desired title
    }

    return $tabs;
}
```