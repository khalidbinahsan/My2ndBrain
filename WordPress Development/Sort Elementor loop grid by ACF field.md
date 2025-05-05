```php
add_action( 'elementor/query/sort_events_by_date', function( $query ) {
    $query->set( 'meta_key', 'event_start_date' );
    $query->set( 'orderby', 'meta_value' );
    $query->set( 'order', 'DESC' );
});
```
Now in the **Query id** field just paste `sort_events_by_date`