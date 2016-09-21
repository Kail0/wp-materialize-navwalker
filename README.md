# wp-materialize-navwalker

**A custom WordPress nav walker class to implement the Materialize CSS nested navigation style in a custom theme**


![Extras](http://i.imgur.com/8J7KG7T.gif)



NOTE
--------------------
This is only a utility class that is intended to format your WordPress theme menu with the correct syntax and classes to utilize
the Mateialize dropdown (nested) navigation, and does't include the required Materialize JS/CSS files. You will have to include them manually.
It also won't work without further changes (the file itself is not enough). Read instructions bellow.

Installation
--------------------
Place **wp_materialize_navwalker.php** in your WordPress theme folder `/wp-content/your-theme/`

Open your WordPress themes **functions.php** file  `/wp-content/your-theme/functions.php` and add the following code:

```php
// Register wp-materialize-navwalker
 require_once get_template_directory() . '/wp_materialize_navwalker.php';
```
Than you need to declare your new menu in your `functions.php` file.

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

Usage
--------------------
Afterthat, update your `wp_nav_menu()` function in `header.php` to use the new walker by adding a "walker" item to the wp_nav_menu array.

```php
 <?php
            wp_nav_menu( array(
                'menu' => 'Primary',
                'theme_location'=>'Primary',
                'menu_class' => 'hide-on-med-and-down',
                'walker' => new wp_materialize_navwalker()
            ));
        ?>
```

Your menu will now be formatted with the correct syntax and classes to implement Materialize dropdown navigation.

jQuery Plugin Initialization
--------------------
You can tweak this. List of initializions can be found in Materialize documentation.

```js
// main dropdown initialization
$('.dropdown-button.main-menu-item').dropdown({
    inDuration: 300,
    outDuration: 225,
    constrain_width: true, // Does not change width of dropdown to that of the activator
    hover: true, // Activate on hover
    belowOrigin: true, // Displays dropdown below the button
    alignment: 'left' // Displays dropdown with edge aligned to the left of button
});
// nested dropdown initialization
$('.dropdown-button.sub-menu-item').dropdown({
    inDuration: 300,
    outDuration: 225,
    constrain_width: false, // Does not change width of dropdown to that of the activator
    hover: true, // Activate on hover
    gutter: ($('.dropdown-content').width() * 3) / 3.05 + 3, // Spacing from edge
    belowOrigin: false, // Displays dropdown below the button
    alignment: 'left' // Displays dropdown with edge aligned to the left of button
});
```

CSS modification
--------------------
You will also need to add one CSS declaration that ensure your nested menu will have the right overflow.

````css
.dropdown-content{
    overflow: visible !important;
}
````

Credits
--------------------
-Wordpress developers
-twittem

Changelog
--------------------
## [1.0.1] - 2016-09-21
### Added
- CSS declaration

### Changed
- README
- Licence

## [1.0.0] - 2016-09-12
### Added
- Initial release