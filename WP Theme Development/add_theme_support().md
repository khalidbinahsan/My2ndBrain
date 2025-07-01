Registers theme support for a given feature.
## [Description](https://developer.wordpress.org/reference/functions/add_theme_support/#description)

Must be called in the theme’s functions.php file to work.  If attached to a hook, it must be [‘after_setup_theme’](https://developer.wordpress.org/reference/hooks/after_setup_theme/).   The [‘init’](https://developer.wordpress.org/reference/hooks/init/) hook may be too late for some features.

Here is the details https://developer.wordpress.org/reference/functions/add_theme_support/

```php
add_theme_support( 'title-tag' );
add_theme_support( 'custom-logo', array(
    'height' => 480,
    'width'  => 720,
) );
```

