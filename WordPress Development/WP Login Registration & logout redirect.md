Add this to redirect after login
```php
add_action('wp_login', 'custom_wp_login_redirect', 10, 2);
function custom_wp_login_redirect($user_login, $user) {
    wp_redirect(home_url('/my-account/'));
    exit;
}

```
Add this to redirect after registration
```php
add_action('user_register', 'custom_registration_redirect');
function custom_registration_redirect($user_id) {
    wp_set_auth_cookie($user_id); // optional auto-login
    wp_redirect(home_url('/my-account/'));
    exit;
}
```
Add this to redirect after logout
```php
add_action('wp_logout', 'custom_logout_redirect');
function custom_logout_redirect() {
    wp_redirect(home_url('/login/')); // Change '/login/' to your login page URL
    exit;
}

```