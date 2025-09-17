To make the elementor tab active with url you can add. Just need to change the query string key
```js
<script>
jQuery(document).ready(function ($) {
  const params = new URLSearchParams(window.location.search);
  const filterValue = params.get("e-filter-a563cd1-case-study-category");

  if (filterValue) {
    const $targetBtn = $(`.e-filter-item[data-filter="${filterValue}"]`);

    if ($targetBtn.length) {
      // First click immediately
      $targetBtn.trigger("click");

      // Second click after 300ms (adjust if needed)
      setTimeout(function () {
        $targetBtn.trigger("click");
      }, 300);
    }
  }
});
</script>
```