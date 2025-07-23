```php
add_action('rest_api_init', function () {
    register_rest_route('custom/v1', '/user-subscription', [
        'methods'  => 'GET',
        'callback' => 'get_user_subscription_data',
        'permission_callback' => function () {           
        $kba_current_user = wp_get_current_user();
            if ( $kba_current_user ) {
                return true;
            }
            return false;
        }
    ]);
});

// REST callback function
function get_user_subscription_data($data) {
      // 🔍 Debug lines (TEMPORARY)
    error_log(print_r($_COOKIE, true));
    error_log('Current user: ' . get_current_user_id());
    $user_id = wp_get_current_user()->ID;
    if (!$user_id) {
        return new WP_Error('no_user', 'User not logged in', ['status' => 401]);
    }

    $user = get_user_by('id', $user_id);
    if (!$user) {
        return new WP_Error('no_user', 'User not found', ['status' => 404]);
    }

    $subscriptions = wcs_get_users_subscriptions($user_id);

    $subs_data = [];

    foreach ($subscriptions as $subscription) {
        /** @var WC_Subscription $subscription */
        $subs_data[] = [
            'subscription_id' => $subscription->get_id(),
            'status' => $subscription->get_status(),
            'items' => array_map(function($item) {
                $feature_terms = get_the_terms($item->get_product_id(), 'feature');
                return [
                    'name' => $item->get_name(),
                    'product_id' => $item->get_product_id(),
                    'qty' => $item->get_quantity(),
                    'features' => is_array($feature_terms)
                        ? array_map(function($term) {
                            return [
                                'id' => $term->term_id,
                                'name' => $term->name,
                                'slug' => $term->slug
                            ];
                        }, $feature_terms)
                        : []
                ];
            }, $subscription->get_items()),
            'start_date' => date("Y-m-d", $subscription->get_time('start')),
            'trial_end' => date("Y-m-d", $subscription->get_time('trial_end')),
            'next_payment' => date("Y-m-d", $subscription->get_time('next_payment')),
            'end_date' => date("Y-m-d", $subscription->get_time('end')),
        ];
    }

    return [
        'user_id' => $user->ID,
        'user_name' => $user->display_name,
        'user_email' => $user->user_email,
        'is_logged_in' => check_current_user(), // should now return true if cookie sent
        'subscriptions' => $subs_data
    ];
}

// CORS headers (allow cookies + credentials)
add_action('rest_api_init', function () {
    remove_filter('rest_pre_serve_request', 'rest_send_cors_headers');
    add_filter('rest_pre_serve_request', function ($value) {
        header("Access-Control-Allow-Origin: https://homai.tp");
        header("Access-Control-Allow-Methods: GET, POST, OPTIONS");
        header("Access-Control-Allow-Headers: Content-Type, Authorization");
        header("Access-Control-Allow-Credentials: true");
        return $value;
    });
});

```