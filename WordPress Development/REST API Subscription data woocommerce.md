```php
add_action('rest_api_init', function () {
    register_rest_route('custom/v1', '/user-subscription/(?P<user_id>\d+)', [
        'methods'  => 'GET',
        'callback' => 'get_user_subscription_data',
        // 'permission_callback' => '__return_true',
        'permission_callback' => function () {
			return is_user_logged_in();
		},
    ]);
});

function get_user_subscription_data($data) {
    $user_id = $data['user_id'];
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
                return [
                    'name' => $item->get_name(),
                    'product_id' => $item->get_product_id(),
                    'qty' => $item->get_quantity()
                ];
            }, $subscription->get_items()),
            'start_date' => $subscription->get_time('start'),
            'trial_end' => $subscription->get_time('trial_end'),
            'next_payment' => $subscription->get_time('next_payment'),
            'end_date' => $subscription->get_time('end'),
        ];
    }

    return [
        'user_id' => $user->ID,
        'user_name' => $user->display_name,
        'user_email' => $user->user_email,
        'is_logged_in' => is_user_logged_in(),
        'subscriptions' => $subs_data
    ];
}

```
For permit any external domain, add this in `functions.php`
```php
add_action('rest_api_init', function() {
    header("Access-Control-Allow-Origin: *"); // In production, use exact domain instead of "*"
    header("Access-Control-Allow-Methods: GET, POST, OPTIONS");
    header("Access-Control-Allow-Headers: application/json, Authorization");
}, 15);
```