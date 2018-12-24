# Custom options container for Carbon Fields

This custom container for [Carbon Fields](https://carbonfields.net/) provides the ability to overwrite the default template file used to render [options panels](https://docs.carbonfields.net/#/containers/theme-options) through a [filter](https://codex.wordpress.org/Plugin_API/Filter_Reference).

## Requirements
- Carbon fields
- Composer

## Installation

1) Install the package via composer by running the command:

`composer require pressmodo/carbon-fields-custom-options-container`

2) Create an options panel and set the container type to `custom_options` instead of `theme_options`. It's required that you set a page file too.


```
Container::make( 'custom_options', 'Theme Options' )
	->set_page_file( 'my-options' )
    ->add_fields( array(
        Field::make( 'text', 'crb_facebook_url') ,
        Field::make( 'textarea', 'crb_footer_text' )
    ) );
```

## Usage

In order to setup a custom file to render options pages you'll need to use the filter: `"cb_theme_options_{$page_file}_container_file"` where `{$page_file}` is the string set with the `set_page_file` method mentioned above (`"cb_theme_options_my-options_container_file"`). 

Through the filter, you need to return the custom file that'll be loaded to render pages. [You can use Carbon Field's existing file as a starting point](https://github.com/htmlburger/carbon-fields/blob/master/templates/Container/common/options-page.php).

```
add_filter( 'cb_theme_options_my-options_container_file', function () {
    return 'path/to/custom-file.php';
});
```