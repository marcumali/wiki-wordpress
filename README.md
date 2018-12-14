# Web Development Tools- WORDPRESS

[MARCUMALI](https://marcumali.github.io) | 
[MAIN](https://github.com/marcumali/wiki) | [HTML](https://github.com/marcumali/wiki-html) | [CSS](https://github.com/marcumali/wiki-css) | [JAVASCRIPT](https://github.com/marcumali/wiki-javascript) | [WORDPRESS](https://github.com/marcumali/wiki-wordpress) | [PHP](https://github.com/marcumali/wiki-php)

Guide and best practice of web development

## BACKEND

* Set most appropriate image sizes in admin and in output
* Forms are submitting data properly & gives the user feedback
* Admin username is not _admin_
* Database has another prefix than `wp_`
* Comments are disabled (if not used)
* WordFence
* Hide wp-config in htaccess
* Disable theme and plugin editor
* Remove unused themes and plugins
* Don’t allow search engines to find page until (remember to turn it on when going live)
* Remove `wp-config-sample.php`
* config.php
	- `define('DISABLE_WP_CRON', 'true');`
* function.php
	- `add_filter('xmlrpc_enabled', '__return_false');`
	- 
	```php
	function remove_version() { 
		return ''; 
	} 
		add_filter('the_generator', 'remove_version');
	```
	- 
	```php
	function wrong_login() { 
		return 'Wrong username or password'; 
	} 
	add_filter('login_errors', 'wrong_login');
	```


## 1. Display posts by specific post type
   This example uses bootstrap column classes.
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
