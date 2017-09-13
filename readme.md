# WP Media Picker jQuery Plugin

This jQuery plugin provides an easy way to generate WP Media frames 
that automatically update hidden <input> elements on selection.

It currently only supports selecting a single image per instance.

It is intended to be used in the WordPress backend, typically inside
<form>...</form> elements, for example, custom meta boxes on edit post
screens.

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



Then wherever you need an image selector, use the following syntax:

```php
<?php
// Get the WordPress attachment ID.
$image_id = get_post_meta( $post_id, $meta_key, true );
// Get an image for an image preview.
$image_url = wp_get_attachment_image_url( $image_id, 'medium' );
?>
<div class="wp-media-picker" 
     data-key="<?php echo esc_attr( $meta_key ); ?>" 
     data-id="<?php echo $image_id; ?>" 
     data-url="<?php echo $image_url; ?>"></div>
```

- data-key -- Sets the name="" attribute on the hidden form element.
- data-id -- Preview image attachment ID. 
- data-url --  URL to the preview image



The plugin does not autoexecute, so we need to do so when scripts are ready: 
```html
<script>
jQuery(document).ready(function($) {
    $(document).wp_media_picker({
        selector: '.wp-media-picker'
    });
});
</script>
```