To get data by REST Api and that only be access able only login user, we must to add this code in header to allow pass the cookie
```php
<script>
   window.wpApiSettings = {
     nonce: "<?php echo wp_create_nonce('wp_rest'); ?>"
   };
 </script>
```
Let create the logged in user api now. I used the Woocommerce and it's subscriptions addons that show the user subscriptions feature
```php
// ======= REST Api start===============

add_action('rest_api_init', function () {
    register_rest_route('custom/v1', '/user-subscription/', [
        'methods'  => 'GET',
        'callback' => 'get_user_subscription_data',
        'permission_callback' => function () {           
            return is_user_logged_in();
        }
    ]);
});

// REST callback function
function get_user_subscription_data() {  
    $user_id = get_current_user_id();
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
        // 'is_logged_in' => check_current_user(), // should now return true if cookie sent
        'subscriptions' => $subs_data
    ];
}

// CORS headers (allow cookies + credentials)
add_action('rest_api_init', function () {
    remove_filter('rest_pre_serve_request', 'rest_send_cors_headers');
    add_filter('rest_pre_serve_request', function ($value) {
        header("Access-Control-Allow-Origin: https://homai.tp");
        header('Access-Control-Allow-Methods: GET, POST, OPTIONS');
        header('Access-Control-Allow-Credentials: true');
        header('Access-Control-Allow-Headers: Content-Type, Authorization, X-WP-Nonce');
        return $value;
    });
});

// Enable cookie authentication in REST
add_filter('rest_authentication_errors', function ($result) {
    if (!empty($result)) {
        return $result;
    }

    if (is_user_logged_in()) {
        return $result;
    }

    return new WP_Error('rest_not_logged_in', 'You are not currently logged in.', ['status' => 401]);
});


// =================== Api end ============================
```
Response will be something like this
```json
{
    "user_id": 1,
    "user_name": "TPAdmin",
    "user_email": "info@homai.com",
    "subscriptions": [
        {
            "subscription_id": 2185,
            "status": "active",
            "items": {
                "37": {
                    "name": "Pro (Most Popular) - 3 Month",
                    "product_id": 2113,
                    "qty": 1,
                    "features": [
                        {
                            "id": 48,
                            "name": "EnhanceIt",
                            "slug": "enhanceit"
                        },
                        {
                            "id": 49,
                            "name": "Remover",
                            "slug": "remover"
                        },
                        {
                            "id": 50,
                            "name": "Sky Color",
                            "slug": "sky-color"
                        }
                    ]
                }
            },
            "start_date": "2025-07-23",
            "trial_end": "1970-01-01",
            "next_payment": "2025-10-23",
            "end_date": "1970-01-01"
        },
        {
            "subscription_id": 2172,
            "status": "cancelled",
            "items": {
                "35": {
                    "name": "Free plan",
                    "product_id": 1878,
                    "qty": 1,
                    "features": [
                        {
                            "id": 48,
                            "name": "EnhanceIt",
                            "slug": "enhanceit"
                        },
                        {
                            "id": 47,
                            "name": "MagicFill",
                            "slug": "magicfill"
                        }
                    ]
                }
            },
            "start_date": "2025-07-22",
            "trial_end": "1970-01-01",
            "next_payment": "1970-01-01",
            "end_date": "2025-07-23"
        },
        {
            "subscription_id": 2134,
            "status": "cancelled",
            "items": {
                "32": {
                    "name": "Enterprise - 2 Month",
                    "product_id": 2102,
                    "qty": 1,
                    "features": [
                        {
                            "id": 48,
                            "name": "EnhanceIt",
                            "slug": "enhanceit"
                        },
                        {
                            "id": 47,
                            "name": "MagicFill",
                            "slug": "magicfill"
                        },
                        {
                            "id": 46,
                            "name": "Redesign",
                            "slug": "redesign"
                        },
                        {
                            "id": 49,
                            "name": "Remover",
                            "slug": "remover"
                        },
                        {
                            "id": 50,
                            "name": "Sky Color",
                            "slug": "sky-color"
                        }
                    ]
                }
            },
            "start_date": "2025-07-21",
            "trial_end": "1970-01-01",
            "next_payment": "1970-01-01",
            "end_date": "2025-07-22"
        }
    ]
}
```
Here is how to call from frontend
```js
<script>
fetch('https://homai.tp/wp-json/custom/v1/user-subscription', {
  method: 'GET',
  headers: {
    'X-WP-Nonce': window.wpApiSettings.nonce
  },
  credentials: 'include'
})
  .then(res => res.json())
  .then(console.log);
</script>
```
Credentials 'include' is important