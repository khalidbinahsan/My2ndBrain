`language_attributes()` This function allow you to load the dynamic `lang` attribute with it's value
```php
<?php
?>
<!DOCTYPE html>
<html <?php language_attributes(); ?> class="no-js">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>

</body>

</html>
```
Here `class="no-js"` is WordPress class that's will help you to not loading the default WP js