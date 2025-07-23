```js
<script>
jQuery(document).ready(function($) {
    // Loop through each password field
    $('input[type="password"]').each(function(index, element) {
        var $passwordField = $(element);

        // Create a unique toggle button for each password field
        var $toggleButton = $('<span class="password-toggle" style="cursor:pointer; margin-left:10px;">👁️</span>');

        // Insert the toggle button after the password field
        $passwordField.after($toggleButton);

        // Bind click event to this specific toggle button
        $toggleButton.on('click', function() {
            var type = $passwordField.attr('type');
            if (type === 'password') {
                $passwordField.attr('type', 'text');
                $toggleButton.text('🙈');
            } else {
                $passwordField.attr('type', 'password');
                $toggleButton.text('👁️');
            }
        });
    });
});
</script>
```
Here is a small css code and adjust if needed
```css
.password-toggle{
	position: absolute;
	right: 0;
	top: 50%;
	transform: translatey(-50%);
}
```