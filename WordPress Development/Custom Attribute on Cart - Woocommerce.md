JS code to add the custom form filed in the Elementor custom add to cart button. You also need to add a custom product price plugin to work with it.
```js
// Quick Donation Global function
	function fieldGenerate(inputs){
		let optionsHtml = '';
		for(let i=0; i<inputs.length; i++){
			optionsHtml += <option value="${inputs[i]}">${inputs[i]}</option>;
		}
		return optionsHtml;
	}
	function quickDonation(formClass, donateTo, country, amount=5) {
		const targetForm = $(formClass + ' form.cart');
		const amountField = $(formClass + ' form.cart .amount');
		const selectField = '<div class="custom-select-wrapper">' +
        '<label for="donate_to">Donate to:</label>' +
        '<select name="donate_to" id="donate_to">' +
			fieldGenerate(donateTo) +
		'</select>' +
		'<label for="donate_country">Country:</label>' +
		'<select name="donate_country" id="donate_country">' +
			fieldGenerate(country)
        '</select>' +
        '</div>';
		targetForm.prepend(selectField);
		amountField.val(amount);
	}
	const gazaDonateTo = ["To where most needed", "Milk for babies", "Hot cooked meals for families", "Medical Aid for those injured and in hospital"];
	const gazaCountry = ["Gaza"];
	quickDonation('.gaza-donation', gazaDonateTo, gazaCountry, 20);
```

```php
// Add custom field data to cart item for specific product ID

add_filter('woocommerce_add_cart_item_data', 'add_custom_fields_to_cart_item', 10, 2);
function add_custom_fields_to_cart_item($cart_item_data, $product_id) {
    // Only apply for product ID 44102
    if ($product_id == 44102 || $product_id == 48589) {
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
    if ($cart_item['product_id'] == 44102 || $cart_item['product_id'] == 48589) {
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
    if ($values['product_id'] == 44102 || $values['product_id'] == 48589) {
        if (isset($values['donate_to'])) {
            wc_add_order_item_meta($item_id, 'Donate To', $values['donate_to']);
        }

        if (isset($values['donate_country'])) {
            wc_add_order_item_meta($item_id, 'Country', $values['donate_country']);
        }
    }
}

```