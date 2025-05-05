Create this shortcode into your `functions.php`
```php
add_shortcode('inline_email_form', 'custom_inline_email_form');

function custom_inline_email_form() {
    ob_start(); ?>

    <form id="email-subscribe-form" method="post">
		<div id="subscriber-form">	
			<input id="subscriber_email" type="email" name="subscriber_email" placeholder="Email address*" required>
			<button id="submit_email" type="submit" name="submit_email">➔</button>
		</div>
    </form>
    <div id="form-response" style="margin-top: 10px;"></div>

    <script>
    document.getElementById('email-subscribe-form').addEventListener('submit', async function(e) {
        e.preventDefault();
        const form = e.target;
        const email = form.subscriber_email.value;

        const responseDiv = document.getElementById('form-response');
        responseDiv.innerHTML = 'Processing...';

        const res = await fetch("<?php echo admin_url('admin-ajax.php'); ?>", {
            method: 'POST',
            headers: {'Content-Type': 'application/x-www-form-urlencoded'},
            body: new URLSearchParams({
                action: 'handle_email_subscription',
                subscriber_email: email
            })
        });

        const data = await res.json();

        responseDiv.innerHTML = data.message;
        responseDiv.style.color = data.success ? 'green' : 'red';
    });
    </script>

    <?php
    return ob_get_clean();
}

// Handle AJAX request
add_action('wp_ajax_nopriv_handle_email_subscription', 'handle_email_subscription_callback');

function handle_email_subscription_callback() {
    $email = isset($_POST['subscriber_email']) ? sanitize_email($_POST['subscriber_email']) : '';

    if (!is_email($email)) {
        wp_send_json(['success' => false, 'message' => 'Invalid email address.']);
    }

    if (email_exists($email)) {
        wp_send_json(['success' => false, 'message' => 'This email is already registered.']);
    }

    $random_password = wp_generate_password();
    $user_id = wp_create_user($email, $random_password, $email);

    if (is_wp_error($user_id)) {
        wp_send_json(['success' => false, 'message' => 'Something went wrong. Please try again.']);
    }

    wp_update_user(['ID' => $user_id, 'role' => 'subscriber']);
    wp_send_json(['success' => true, 'message' => 'Thank you for subscribing!']);
}

```
Some style
```css
#subscriber-form{
	display: flex;
	gap: 3px;
	border: 1px solid #d1d1d1;
	padding: 5px;
	border-radius: 5px;
}
#subscriber_email {
	border: 0;
	outline: 0;
}
#submit_email {
	padding: 10px 15px;
	border-radius: 5px;
	border: 0;
	background: black;
	color: #fff;
}
#submit_email:hover{
	background: #E9C522;
	color: black;
}
```