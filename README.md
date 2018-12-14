# Web Development Tools- WORDPRESS

[MARCUMALI](https://marcumali.github.io) | 
[MAIN](https://github.com/marcumali/wiki) | [HTML](https://github.com/marcumali/wiki-html) | [CSS](https://github.com/marcumali/wiki-css) | [JAVASCRIPT](https://github.com/marcumali/wiki-javascript) | [WORDPRESS](https://github.com/marcumali/wiki-wordpress) | [PHP](https://github.com/marcumali/wiki-php)

Guide and best practice of web development

## 1. Display posts by specific category
   This example uses bootstrap column grid
```php
<?php

    $i = 0;
	$args = array(
	'post_type'   => 'room',
        'post_status' => 'publish',
        'orderby' => '',
	);

	$wpQuery = new WP_Query( $args );
	$postList = $wpQuery->posts;

?>

<?php if( $postList ) : ?>
    <?php foreach( $postList as $item ) :
        $link = get_permalink( $item );
        $image = get_the_post_thumbnail( $item, 'full' );

        $col1st = 'col-md-7 col-md-push-5';
        $col2nd = 'col-md-5 col-md-pull-7';
        if ( $i % 2 == 0 ) {
            $col1st = '';
            $col2nd = '';
        }
    ?>
    <div class="row">
        <div class="col-md-7 <?php echo $col1st; ?>">
            <div>
                <?php echo $image; ?>
            </div>
        </div>
        <div class="col-md-5 <?php echo $col2nd; ?>">
          <h2><?php echo $item->post_title; ?></h2>
          <?php echo apply_filters( 'the_content', $item->post_content ); ?>
        </div>
    </div>
    <?php $i++; endforeach; ?>
<?php endif; ?>
```
