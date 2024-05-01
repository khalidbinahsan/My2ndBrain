add this code snippet to your **functions.php** file

```php
function display_last_three_posts() {
    $args = array(
        'posts_per_page' => 3,
        'orderby'        => 'date',
        'order'          => 'DESC',
    );

    $posts_query = new WP_Query( $args );

    if ( $posts_query->have_posts() ) {
        $output = '<ul style="padding: 0;">';

        while ( $posts_query->have_posts() ) {
            $posts_query->the_post();
            $title = get_the_title();
            $short_title = (strlen($title) > 130) ? substr($title, 0, 130) . '...' : $title;
            $output .= '<li class="footer-post">';
            $output .= '<a class="post-content" href="' . get_permalink() . '">';
            $output .= '<div class="footer-post-img">'.get_the_post_thumbnail( get_the_ID(), 'thumbnail' ) . '</div>';
            $output .= '<div class="footer-post-title">'. $short_title . '</div>';
            $output .= '</a></li>';
        }

        $output .= '</ul>';

        wp_reset_postdata();

        return $output;
    } else {
        return 'No posts found';
    }
}
add_shortcode( 'last_three_posts', 'display_last_three_posts' );
```

Here is some **CSS** code
```css
.footer-post .post-content img{
	max-width: 40px;
	border-radius: 2px;
}
.footer-post{
	list-style: none;
	margin-bottom: 10px;
}
.post-content{
	display: flex;
	justify-content: center;
	align-items: center;
	gap: 10px;
}
.footer-post-title{
	font-family: "Bangla1", Sans-serif;
	color: #fff;
}
.post-content:hover .footer-post-title{
	color: #AF2724; 
}
```