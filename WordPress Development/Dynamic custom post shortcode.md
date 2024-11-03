```php
function custom_post_shortcode($atts) {
    // Attributes
    $atts = shortcode_atts(
        array(
            'post_type' => 'post',
            'posts_per_page' => '5',
        ),
        $atts,
        'custom_post'
    );

    // Query
    $query = new WP_Query(array(
        'post_type' => $atts['post_type'],
        'posts_per_page' => $atts['posts_per_page']
    ));

    // Output
    $output = '<ul class="custom-posts">';
    if ($query->have_posts()) {
        while ($query->have_posts()) {
            $query->the_post();

            // Limit the title to 10 characters and add "..."
            $title = get_the_title();
            if (strlen($title) > 10) {
                $title = substr($title, 0, 130) . '...';
            }

            $output .= '<li class="custom-post-item">';
            $output .= '<a href="' . get_permalink() . '">' . '<svg aria-hidden="true" class="e-font-icon-svg e-fas-check-circle" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg"><path d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z"></path></svg>' . $title . '</a>';
            $output .= '<p>' . get_the_excerpt() . '</p>';
            $output .= '</li>';
        }
        wp_reset_postdata();
    } else {
        $output .= '<p>No posts found</p>';
    }
    $output .= '</ul>';

    return $output;
}
add_shortcode('custom_post', 'custom_post_shortcode');
```
Add some css
```css
/* === Custom Post Item === */
.custom-posts{
	padding: 0 !important;
	font-family: "Bangla1", Sans-serif;
	font-size: 16px;
}
.custom-post-item {
	list-style: none;
}
.custom-post-item a {
	color: #1B1464;
}
.custom-post-item a:hover{
	color: #D00000;
	text-decoration: underline;
}
.custom-post-item a svg{
	max-width: 16px;
	margin-right: 10px;
	fill: #609513;
}
```