add this code into the `functions.php` and replace the template ids with your one.
```php
add_shortcode('custom_elementor_slider', function() {
    // Replace these with your actual template IDs
    $template_ids = [211, 214, 302, 312];

    ob_start();
    ?>
    <div class="custom-swiper swiper">
      <div class="swiper-wrapper">
        <?php foreach ($template_ids as $id): ?>
          <div class="swiper-slide <?php echo 'slider-is-' . $id; ?>">
            <?php
              echo Elementor\Plugin::instance()->frontend->get_builder_content($id);
            ?>
          </div>
        <?php endforeach; ?>
      </div>

      <!-- Optional: Pagination & Navigation -->
      <div class="swiper-pagination"></div>
    </div>

    return ob_get_clean();
});
```
Some of the swiper slider here..
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
      mousewheel: true,
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