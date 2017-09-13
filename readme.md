# WP Media Picker jQuery Plugin

This jQuery plugin provides an easy way to insert wp.media pickers 
into the WordPress backend.

It currently only supports selecting single image per selector.

The plugin converts a selector element into a hidden input field

### Install

```
bower install wp-media-picker-jquery
```

### Usage

First, enqueue the javascript file in **admin_enqueue_scripts** so that it
is available in the backend.

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