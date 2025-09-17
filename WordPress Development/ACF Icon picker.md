You can take the icon picker field and allow only the media upload svg icon options then get it with the following code in the Elementor loop item
```php
add_shortcode('acf_icon', function() {
    if (!function_exists('get_field')) return '';

    $icon_url = get_field('field_slug');
    if (empty($icon_url) || !filter_var($icon_url, FILTER_VALIDATE_URL)) return '';

    return '<img src="' . esc_url($icon_url) . '" alt="Acf Icon" class="acf-icon" />';
});
```
Paste the shortcode `[acf_icon]`