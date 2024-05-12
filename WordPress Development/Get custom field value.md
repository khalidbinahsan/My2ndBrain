You can set custom field value on your page or post by activate it from the screen option. And here is the code to get that field value easily.
```php
<?php
// Get the current page ID
$page_id = get_the_ID();
// Get the custom field value for the current page
$header_value = get_post_meta($page_id, 'custom_header_field', true);
// Output the custom field value in the header
if (!empty($header_value)) {
    echo '<div class="custom-header">' . esc_html($header_value) . '</div>';
}
?>
```