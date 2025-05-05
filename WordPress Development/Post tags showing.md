```php
function a3trips_recent_tags_shortcode($atts) {
    $atts = shortcode_atts(array(
        'number' => 10, // Default to 10 tags
        'hide_empty' => false, // Show tags even if they have no posts
    ), $atts);

    $recent_tags = get_terms(array(
        'taxonomy' => 'post_tag',
        'orderby' => 'id',
        'order' => 'DESC',
        'number' => $atts['number'],
        'hide_empty' => $atts['hide_empty'],
    ));

    if (empty($recent_tags) || is_wp_error($recent_tags)) {
        return '<p>No tags found.</p>';
    }

    $output = '<ul class="recent-tags">';
    foreach ($recent_tags as $tag) {
        $tag_link = esc_url(get_tag_link($tag->term_id));
        $tag_name = esc_html($tag->name);
        $output .= "<li><a href='{$tag_link}'>{$tag_name}</a></li>";
    }

    $output .= '</ul>';
    return $output;
}
add_shortcode('recent_tags', 'a3trips_recent_tags_shortcode');
```