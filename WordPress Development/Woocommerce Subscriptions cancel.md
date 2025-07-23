To cancel all previous plan when user purchase a new plan in woocommerce subscriptions, add the following code
```php
add_action( 'woocommerce_checkout_subscription_created', 'cancel_previous_subscriptions', 10, 3 );
function cancel_previous_subscriptions( $subscription, $order, $recurring_cart ) {
    $user_id = $subscription->get_user_id();

    if ( ! $user_id ) return;

    $new_subscription_id = $subscription->get_id();

    // Get all active subscriptions for the user
    $subscriptions = wcs_get_users_subscriptions( $user_id );

    foreach ( $subscriptions as $sub_id => $sub ) {
        if ( $sub_id === $new_subscription_id ) continue;

        if ( $sub->has_status( array( 'active', 'pending', 'on-hold' ) ) ) {
            $sub->update_status( 'cancelled', 'Auto-cancelled due to new subscription purchase.' );
        }
    }
}
```