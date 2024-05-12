Well, if you want to change your custom post type term automatically depending on any date of condition, here is some example to add on your theme **functions.php** file..

```php
function update_event_taxonomy_terms() {
    $today = current_time('Ymd'); // Get today's date in 'YYYYMMDD' format.
    $args = array(
        'post_type' => 'event', // Custom post type
        'posts_per_page' => -1, // Process every event
        'meta_query' => array(
            array(
                'key' => 'event_start_date',
                'value' => $today,
                'compare' => '<',
                'type' => 'DATE'
            )
        ),
        'tax_query' => array(
            array(
                'taxonomy' => 'event_category',
                'field' => 'slug',
                'terms' => 'upcoming-events',
            )
        )
    );

    $events = new WP_Query($args);
    if ($events->have_posts()) {
        while ($events->have_posts()) {
            $events->the_post();
            $event_id = get_the_ID();
            // Remove from 'Upcoming Events'
            wp_remove_object_terms($event_id, 'upcoming-events', 'event_category');
            // Add to 'Past Events'
            wp_set_object_terms($event_id, 'past-events', 'event_category', true);
        }
    }
    wp_reset_postdata();
}
```

Now add a corn job 

```php
if (!wp_next_scheduled('update_event_taxonomy_terms_hook')) {
    wp_schedule_event(time(), 'daily', 'update_event_taxonomy_terms_hook');
}

add_action('update_event_taxonomy_terms_hook', 'update_event_taxonomy_terms');
```