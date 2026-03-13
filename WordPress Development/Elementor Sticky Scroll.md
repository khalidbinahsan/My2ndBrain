Here is some simple jquery code to make a sticky scroll
```js
<script>
  jQuery(function($) {
    $(window).on("scroll", function() {
        $(".img-container-parent").each(function() {
            var triggerPos = $(this).offset().top - 100;
            var scrollPos = $(window).scrollTop();
            if (scrollPos >= triggerPos) {
                var imgNumber = $(this).data("img");
                $(".image-container").removeClass("active");
                $(".image-container-" + imgNumber).addClass("active");
            }
        });

    });
});
</script>
```
Just give a class to the parent container of the left side is **"img-container-parent"** and take a attribute on it like **"data-img=1", "data-img=2", "data-img=3","data-img=4"** something like this. On the right side on the images, give the class is "image-container image-container-1", "image-container image-container-2", "image-container image-container-3", "image-container image-container-4" something like this and make it sticky top with elementor. That's it. It will work then. Here is some css you need to add
```css
.image-container{
    opacity: 0;
    transition: opacity 0.5s ease;
    display: none;
}
.image-container.active {
    opacity: 1;
    z-index: 2;
    display: block;
}
```