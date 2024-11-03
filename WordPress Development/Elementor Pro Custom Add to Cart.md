First of all need to add your custom filed to the Elementor pro Custom Add to Cart button form with jQuery
```js
// Target the WooCommerce Add to Cart form
    let addToCartForm = $('.appeal-donation form.cart');

    // Create a custom select input
    let customSelectInput = '<div class="custom-select-wrapper">' +
        '<label for="donate_to">Donate to:</label>' +
        '<select name="donate_to" id="donate_to">' +
        '<option value="Where Most Needed">Where Most Needed</option>' +
        '<option value="Water Wells">Water Wells</option>' +
		'<option value="Water Pumps">Water Pumps</option>' +
		'<option value="Zakat">Zakat</option>' +
		'<option value="Sadaqah">Sadaqah</option>' +
        '</select>' +
		'<label for="donate_country">Country:</label>' +
		'<select name="donate_country" id="donate_country">' +
		'<option value="Bangladesh">Bangladesh</option>' +
		'<option value="Pakistan">Pakistan</option>' +
		'<option value="Africa">Africa</option>' +
		'<option value="Gaza">Gaza</option>' +
        '</select>' +
        '</div>';

    // Inject the custom select input into the form
    addToCartForm.prepend(customSelectInput);
```
Now add the following function to your theme functions.php
```php
// Add custom field data to cart item for specific product ID
add_filter('woocommerce_add_cart_item_data', 'add_custom_fields_to_cart_item', 10, 2);
function add_custom_fields_to_cart_item($cart_item_data, $product_id) {
    // Only apply for product ID 44102
    if ($product_id == 44102) {
        if (isset($_POST['donate_to'])) {
            $cart_item_data['donate_to'] = sanitize_text_field($_POST['donate_to']);
        }

        if (isset($_POST['donate_country'])) {
            $cart_item_data['donate_country'] = sanitize_text_field($_POST['donate_country']);
        }

        // Generate a unique key to prevent merging of cart items with different custom fields
        $cart_item_data['unique_key'] = md5(microtime().rand());
    }

    return $cart_item_data;
}

// Display custom field data in the cart and checkout pages
add_filter('woocommerce_get_item_data', 'display_custom_fields_cart_checkout', 10, 2);
function display_custom_fields_cart_checkout($item_data, $cart_item) {
    // Only display for product ID 44102
    if ($cart_item['product_id'] == 44102) {
        if (isset($cart_item['donate_to'])) {
            $item_data[] = array(
                'name' => 'Donate To',
                'value' => wc_clean($cart_item['donate_to'])
            );
        }

        if (isset($cart_item['donate_country'])) {
            $item_data[] = array(
                'name' => 'Country',
                'value' => wc_clean($cart_item['donate_country'])
            );
        }
    }

    return $item_data;
}

// Add custom field data to the order on checkout
add_action('woocommerce_add_order_item_meta', 'save_custom_fields_order_meta', 10, 2);
function save_custom_fields_order_meta($item_id, $values) {
    // Only save for product ID 44102
    if ($values['product_id'] == 44102) {
        if (isset($values['donate_to'])) {
            wc_add_order_item_meta($item_id, 'Donate To', $values['donate_to']);
        }

        if (isset($values['donate_country'])) {
            wc_add_order_item_meta($item_id, 'Country', $values['donate_country']);
        }
    }
}

```

Done! now if you add to cart any item, the additional field data will be assign as the product attribute.