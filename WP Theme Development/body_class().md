Add this function `body_class()` in body to load the WP dynamic classes
```php
<?php
/*
* This template for displaying header
*/
?>
<!DOCTYPE html>
<html <?php language_attributes(); ?> class="no-js">
<head>
    <meta charset="<?php bloginfo('charset'); ?>">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <?php wp_head(); ?>
</head>
<body <?php body_class(); ?>>
   

<?php wp_footer(); ?>
</body>
</html>
```