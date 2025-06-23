add this code into the `functions.php` and replace the template ids with your one.
```php
add_shortcode('custom_elementor_slider', function($atts) {
    // Define default attributes
    $atts = shortcode_atts([
        'template_ids' => '', // comma-separated
        'class' => 'custom-swiper',
    ], $atts);

    // Convert comma-separated IDs to an array and sanitize
    $template_ids = array_map('absint', explode(',', $atts['template_ids']));
    $wrapper_class = sanitize_html_class($atts['class']);

    ob_start();
    ?>
    <div class="<?php echo esc_attr($wrapper_class); ?> swiper">
        <div class="swiper-wrapper">
            <?php foreach ($template_ids as $id): ?>
                <div class="swiper-slide <?php echo esc_attr('slider-is-' . $id); ?>">
                    <?php echo Elementor\Plugin::instance()->frontend->get_builder_content($id); ?>
                </div>
            <?php endforeach; ?>
        </div>

        <!-- Optional: Pagination -->
        <div class="swiper-pagination"></div>
    </div>
    <?php
    return ob_get_clean();
});
```
So your shortcode would be something like this `[custom_elementor_slider template_ids="211,214,302" class="custom-swiper"]` 

Some of the swiper slider js here..
```js
<script>
  document.addEventListener("DOMContentLoaded", function () {
    const swiper = new Swiper('.custom-swiper', {
      speed: 1000,
      loop: false, // Must be false to detect last slide
      slidesPerView: 1,
      spaceBetween: 0,
      pagination: {
        el: '.swiper-pagination',
        clickable: true,
      },
      navigation: {
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev',
      },
    });
</script>
```

Make sure it's loaded properly
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@9/swiper-bundle.min.css"/>
<script src="https://cdn.jsdelivr.net/npm/swiper@9/swiper-bundle.min.js"></script>
```
Add your CSS
```css
 .swiper-slide {
    display: flex;
    align-items: center;
    justify-content: center;
}   
```