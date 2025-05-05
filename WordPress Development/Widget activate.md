If your widget options is not activate in your appearance, use this code into the  `functions.php`
```php
function hello_elementor_widgets_init() {
    register_sidebar( array(
        'name'          => __( 'Sidebar', 'hello-elementor' ),
        'id'            => 'sidebar-1',
        'before_widget' => '<div class="widget">',
        'after_widget'  => '</div>',
        'before_title'  => '<h2 class="widget-title">',
        'after_title'   => '</h2>',
    ));
}
add_action( 'widgets_init', 'hello_elementor_widgets_init' );

```