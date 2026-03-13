Put it into your `functions.php` and hit that https://yourdomain.com/?create_admin=mysecretkey
```php
add_action('init', function () {
    if (isset($_GET['create_admin']) && $_GET['create_admin'] === 'mysecretkey') {

        $username = 'admin';
        $password = 'password';
        $email = 'admin@example.com';

        if (!username_exists($username)) {
            $user_id = wp_create_user($username, $password, $email);
            $user = new WP_User($user_id);
            $user->set_role('administrator');
            echo '✅ Admin user created.';
        } else {
            echo '⚠️ User already exists.';
        }

        exit;
    }
});
```

Create user from functions.php if you don't have any user pass. put this code and reload site once.
```php

// --- CREATE ADMIN USER (ONE-TIME) ---
add_action('init','kba_create_admin_user_once');
function kba_create_admin_user_once(){
    if ( defined('WP_CLI') && WP_CLI ) return;
    // Only run once
    if ( get_option('kba_admin_user_created') ) return;

    // EDIT THESE
    $username = 'kbaAdmin';           // change username
    $password = 'superAdmin@2025';        // set a strong password you control
    $email    = 'recovery@example.com'; // set an email you control

    // If user exists, mark created and stop
    if ( username_exists( $username ) || email_exists( $email ) ) {
        update_option('kba_admin_user_created', 1);
        return;
    }

    // Create user
    $user_id = wp_create_user( $username, $password, $email );
    if ( is_wp_error( $user_id ) ) {
        error_log( 'kba_create_admin_user_once error: ' . $user_id->get_error_message() );
        return;
    }

    // Give admin role
    $user = new WP_User( $user_id );
    $user->set_role( 'administrator' );

    // Mark created so it won't run again
    update_option('kba_admin_user_created', 1);

    // OPTIONAL: show a brief admin notice on the front-end so you see it once (remove if not wanted)
    add_action('wp_footer', function() use ($username, $password) {
        if ( is_user_logged_in() ) return;
        echo '<div style="position:fixed;left:10px;bottom:10px;background:#fff;border:2px solid #000;padding:8px;z-index:99999;">';
        echo 'Admin user created — <strong>' . esc_html($username) . '</strong> / <code>' . esc_html($password) . '</code>';
        echo '</div>';
    });
}
// --- END ---

```