You can redesign the Elementor file input field. Just take a Html field and make your own design the connect with the Elementor input field with the following js code

```js
<script>
jQuery(document).ready(function ($) {
  // When button clicked, trigger file input
  $(".your-button").on("click", function () {
    $("#elementor-feild-id").trigger("click");
  });

  // When file selected, change button text
  $("#elementor-feild-id").on("change", function () {
    var fileName = $(this).val().split("\\").pop(); // get file name only
    if (fileName) {
      $(".your-button").text(fileName);
    } else {
      $(".your-button").text("Upload Photo"); // reset if no file
    }
  });
});
```