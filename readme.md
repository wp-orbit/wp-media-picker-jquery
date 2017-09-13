# WP Media Picker jQuery Plugin

This jQuery plugin provides an easy way to generate WP Media frames 
that automatically update hidden &lt;input> elements on selection.

It is intended to be used in the WordPress backend, typically inside
&lt;form> elements, for example, in options pages or custom meta boxes on 
edit post screens.

Currently only selecting a single image is selected per instance.

### Installation

```
bower install wp-media-picker-jquery --save
```

Copy the javascript file to your plugin or theme.

Enqueue the javascript file in **admin_enqueue_scripts** so that it
is available in the backend.

```php
<?php
add_action( 'admin_enqueue_scripts', function() {
    $url = '/path/to/wp-media-picker-jquery.js';
    wp_enqueue_script( 'wp-media-picker-jquery', $url, ['jquery'], null, true );
});
```
### Usage

Add CSS class **wp-media-picker** to an element, and provide the data-key, data-id, 
data-url attributes.
 
Use the following syntax wherever you want to generate an image selector:

```php
<?php
// An option or meta key, also sets the name attribute, via <input type="hidden" name="{$option_key}">
$option_key = '_background_image';
// Get the WordPress attachment ID.
$image_id = get_post_meta( $post_id, $option_key, true );
// Get an image for an image preview.
$image_url = wp_get_attachment_image_url( $image_id, 'medium' );
?>
<div class="wp-media-picker" 
     data-key="<?php echo esc_attr( $option_key ); ?>" 
     data-id="<?php echo $image_id; ?>" 
     data-url="<?php echo $image_url; ?>"></div>
```

- '.wp-media-picker' is the selector 
- data-key -- Sets the name="" attribute on the hidden form element.
- data-id -- Preview image attachment ID. 
- data-url --  URL to the preview image


### After Selecting an Image

When you select an image, the hidden input element will be automatically updated. 
WordPress media attachment IDs are stored as the value.
If an image is removed, the value is set to an empty string.

### Form Processing

When POSTed inside of &lt;form> elements, the data is exposed like any other
PHP form data:

```php
<?php
// Is our meta key present in the $_POST array?
if ( isset( $_POST[$meta_key] ) ) {
    if ( empty( $_POST[$meta_key] ) ) {
        // Remove the image from meta or option...
    } else {
        $image_id = $_POST[$meta_key];
        // Do something with the image ID.
    }
}
``` 