To apply all the post type
```php
function sort_all_custom_post_types_admin_by_date( $query ) {
    global $pagenow;

    if ( is_admin() && $pagenow === 'edit.php' && ! isset( $_GET['orderby'] ) ) {
        // Only apply if a specific post type is set (to avoid affecting other admin pages)
        if ( isset( $_GET['post_type'] ) ) {
            $query->set( 'orderby', 'date' );
            $query->set( 'order', 'DESC' );
        } else {
            // Also apply for the default 'post' type
            $query->set( 'orderby', 'date' );
            $query->set( 'order', 'DESC' );
        }
    }
}
add_action( 'pre_get_posts', 'sort_all_custom_post_types_admin_by_date' );

```
For individual post type
```php
function sort_registration_admin_by_date( $query ) {
    global $pagenow;

    if ( is_admin() && $pagenow === 'edit.php' && isset( $_GET['post_type'] ) && $_GET['post_type'] === 'registration' && ! isset( $_GET['orderby'] ) ) {
        $query->set( 'orderby', 'date' );
        $query->set( 'order', 'DESC' );
    }
}
add_action( 'pre_get_posts', 'sort_registration_admin_by_date' );
```