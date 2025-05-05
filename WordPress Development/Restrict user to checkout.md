```php
function restrict_checkout_for_specific_roles() {
    if (is_admin()) return; // Do not apply in admin area

    if (is_checkout() || is_cart()) {
        $user = wp_get_current_user();
        $allowed_roles = array('wholesale_customer', 'Distributor_Customer');

        if (!array_intersect($allowed_roles, $user->roles)) {
            wc_add_notice(__('Only authorized wholesale customers can place orders. Please log in or register.', 'woocommerce'), 'error');
            wp_redirect(home_url()); // Redirect to homepage or another page
            exit;
        }
    }
}
add_action('template_redirect', 'restrict_checkout_for_specific_roles');
```