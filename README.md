# wp-materialize-navwalker
======================
**A custom WordPress nav walker class to "fully" implement the Materialize CSS nested navigation style in a custom theme using the WordPress manager**


![Extras](http://i.imgur.com/8J7KG7T.gif)



NOTE
----
This is only a utility class that is intended to format your WordPress theme menu with the correct syntax and classes to utilize
the Mateialize dropdown (nested) navigation, and does't include the required Materialize JS/CSS files.
You will have to include them manually.

Installation
------------
Place **wp_materialize_navwalker.php** in your WordPress theme folder `/wp-content/your-theme/`

Open your WordPress themes **functions.php** file  `/wp-content/your-theme/functions.php` and add the following code:

```php
// Register Custom Navigation Walker
 require_once get_template_directory() . '/wp-materialize-navwalker.php';
```

Usage
------------
Update your `wp_nav_menu()` function in `header.php` to use the new walker by adding a "walker" item to the wp_nav_menu array.

```php
 <?php
            wp_nav_menu( array(
                'menu' => 'Primary',
                'theme_location'=>'Primary',
                'menu_class' => 'hide-on-med-and-down',
                'walker' => new wp-materialize-navwalker()
            ));
        ?>
```

Your menu will now be formatted with the correct syntax and classes to implement Materialize dropdown navigation.

You will also want to declare your new menu in your `functions.php` file.

```php
register_nav_menus(
    array(
        'Primary'   =>  __( 'Primary Menu', 'THEMENAME' ),
        // Register the Primary menu and Drawer menu
        // Theme uses wp_nav_menu() in TWO locations.
        // Copy and paste the line above right here if you want to make another menu,
        // just change the 'primary' to another name
    )
);
```

Changelog
----
## [1.0.0] - 2016-09-12
### Added
- Initial release