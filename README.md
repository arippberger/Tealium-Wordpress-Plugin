Tealium Wordpress Plugin
========================

To install:

* Install from the Wordpress plugin repository, or copy to your wp-content/plugins folder.
* Enable through the plugins section within Wordpress.
* Paste your Tealium code into 'Tealium Settings' under Settings in Wordpress and save.
* That's it!

Optional steps:

* The position of the Tealium tag can be selected.
* If there are items you wish to exclude from your data object, add the keys as a comma separated list.

Action examples
---------------

There are a couple of actions that can be used to manipulate the Tealium tag or data object in your themes functions.php file or within your own plugin.

For example:

```php
/*
 * Dynamically add data to the Tealium data object
 */
function addToDataObject() {
	global $utagdata;
	
	// Add the current PHP version to the data layer
	$utagdata['php_version'] = phpversion();
	
	// Add a timestamp to the data layer
	$utagdata['timestamp'] = time();
}
add_action( 'tealium_addToDataObject', 'addToDataObject' );

/*
 * Switch Tealium environment based on website URL
 */
function switchEnvironment() {
	global $tealiumtag;
	
	if ( get_site_url() == 'http://dev.mywebsite.com' ) {
		$tealiumtag = str_replace( '/prod/', '/dev/', $tealiumtag );
	}
}
add_action( 'tealium_tagCode', 'switchEnvironment' );
```

