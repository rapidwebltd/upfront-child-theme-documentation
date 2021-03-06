# File Structure

##Folders
### element-styles
Separate CSS files for styling individual elements to be used on a page such as button styles, navigation styles, etc

### fonts
Any custom web fonts go here.

### global-regions
Global Regions are sections of a web page that occur on every single page such as the header, navigation or footer sections. This allows for edits to be made once and will affect the rest of the pages that the global regions are used on. 

### icon-fonts
Any custom icon fonts go here.

### images
Images are kept here that are used within the theme, such as region background images, etc.

### languages
Portable Object Templates are kept here which lists localisable text. [Source](http://wordpress.stackexchange.com/a/710).

### layouts
Page specific layouts are stored here such as how login pages, 404 pages, etc should look by default.

### postlayouts
Blog post specific layouts are stored here such as how a single post is laid out by default.

### templates
Similar to global-regions, these are portions of layouts to be used frequently between different pages. Such as having a author bio section on post pages.

### ui
Empty folder? (Investigating...)

## Key files

### functions.php

This file behaves similarly to `functions.php` for WordPress themes.

A class is defined in this function which represents the Upfront child theme and, in fact, extends the existing `Upfront_ChildTheme` class. For creating a new theme, it is important to change:

1. The class name, in the classes definition
2. The return value of the public `get_prefix` method.
3. The call to the `ClassName::serve()` method at the bottom of the file.

### page_tpl-*.php files

These files appear to build up the rendered content for a specific page, with a specific template defined.

The following is an example 'About' page. File name: `page_tpl-about.php`.

```php
<?php
/**
 * Template Name: About Page template
 *
 * @package WordPress
 * @subpackage about
 */

the_post();
$layout = Upfront_Output::get_layout(array('specificity' => 'single-page-about'));

get_header();
echo $layout->apply_layout();
get_footer();
?>
```

The important point to note here is that `specificity` identifies the template file from the `layouts/` directory (minus the `.php`).

### screenshot.png
A preview image of the theme, same functionality as standard WordPress themes. [Read More](https://codex.wordpress.org/Theme_Development#Screenshot).

### settings.php

This file contains a large PHP array that defines global theme settings. The function of each array key is defined below.

* `typography` - Typography styling (CSS) 
* `layout_style` - Main layout styling (CSS)
* `layout_properties` - Defines the default background colour, container width, and various grid settings such as guttering (JSON formatted)
* `theme_colors` - Default theme colours, which can be overridden in the Upfront colour palette (JSON formatted)
* `theme_fonts` - Fonts that are available in the Upfront editor font dropdown for this theme (JSON formatted)
* `menus` - Default theme menus, customisable via the Upfront editor (JSON formatted)
 * Menu `items` are links to WordPress posts
* `global_regions` - Appears to define the default header and footer (?) (JSON formatted)
* `required_pages` - Defines the default pages to be created when the theme is active (or activated?) (JSON formatted)
 * Each page has its `name`, `slug` and `layout` defined.
 * The `layout` refers to a file (minus the `.php` extension) within the `layouts/` directory.
* `responsive_settings` - Seems similar to the `responsive` array key, but without escaping? Unknown purpose. (JSON formatted)
* `post_image_variants` - Perhaps related to how WordPress stores details in its image library about sizes, cropping etc. (JSON formatted)
* `button_presets` - Defines default buttons and their styling for use in the theme (JSON formatted)
* `responsive` - Defines breakpoints and CSS for those breakpoints (JSON formatted)
* `accordian_presets` - Defines styling of the Upfront accordion element for this theme (JSON formatted)
* `icon_fonts` - Defines icon/symbolic font(s) used in this theme, similar to FontAwesome (JSON formatted)
* `tab_presets` - Define styling of tabs related elements in this theme (JSON formatted)

### style.css
A stylesheet that contains the information about the theme in the comments, such as theme name, author, URLs, etc.
