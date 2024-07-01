---
title: Overview of Content Plugins
---
Content Plugins in <SwmToken path="/wp-content/plugins/hello.php" pos="8:7:7" line-data="Plugin URI: http://wordpress.org/plugins/hello-dolly/">`wordpress`</SwmToken>, such as those found in the <SwmPath>[wp-content/plugins//](/wp-content/plugins//)</SwmPath> directory, are pieces of software that add specific features or functionalities to the website. They are written in PHP and integrate seamlessly with <SwmToken path="/wp-content/plugins/hello.php" pos="8:7:7" line-data="Plugin URI: http://wordpress.org/plugins/hello-dolly/">`wordpress`</SwmToken>. These plugins allow for customization and control over the website, extending the core functionality of <SwmToken path="/wp-content/plugins/hello.php" pos="8:7:7" line-data="Plugin URI: http://wordpress.org/plugins/hello-dolly/">`wordpress`</SwmToken>.

<SwmSnippet path="/wp-content/plugins/hello.php" line="1">

---

For instance, the 'Hello Dolly' plugin, when activated, displays lyrics from the song 'Hello, Dolly' in the upper right of your admin screen on every page.

```hack
<?php
/**
 * @package Hello_Dolly
 * @version 1.7.2
 */
/*
Plugin Name: Hello Dolly
Plugin URI: http://wordpress.org/plugins/hello-dolly/
Description: This is not just a plugin, it symbolizes the hope and enthusiasm of an entire generation summed up in two words sung most famously by Louis Armstrong: Hello, Dolly. When activated you will randomly see a lyric from <cite>Hello, Dolly</cite> in the upper right of your admin screen on every page.
Author: Matt Mullenweg
Version: 1.7.2
Author URI: http://ma.tt/
*/
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet-admin.php" line="1284">

---

Another example is the 'Akismet' plugin, which helps protect your blog from spam. It modifies its own description based on whether it's active and properly configured or not.

```hack
	/**
	 * When Akismet is active, remove the "Activate Akismet" step from the plugin description.
	 */
	public static function modify_plugin_description( $all_plugins ) {
		if ( isset( $all_plugins['akismet/akismet.php'] ) ) {
			if ( Akismet::get_api_key() ) {
				$all_plugins['akismet/akismet.php']['Description'] = __( 'Used by millions, Akismet is quite possibly the best way in the world to <strong>protect your blog from spam</strong>. Your site is fully configured and being protected, even while you sleep.', 'akismet' );
			}
			else {
				$all_plugins['akismet/akismet.php']['Description'] = __( 'Used by millions, Akismet is quite possibly the best way in the world to <strong>protect your blog from spam</strong>. It keeps your site protected even while you sleep. To get started, just go to <a href="admin.php?page=akismet-key-config">your Akismet Settings page</a> to set up your API key.', 'akismet' );
			}
		}

		return $all_plugins;
	}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/hello.php" line="1">

---

# Hello Dolly Plugin

The 'Hello Dolly' plugin is an example of a content plugin. It adds a random lyric from the song 'Hello, Dolly' to the admin screen of the <SwmToken path="/wp-content/plugins/hello.php" pos="8:7:7" line-data="Plugin URI: http://wordpress.org/plugins/hello-dolly/">`wordpress`</SwmToken> website. The plugin is activated by adding an action to the <SwmToken path="/wp-content/plugins/hello.php" pos="68:22:22" line-data="// Now we set that function up to execute when the admin_notices action is called.">`admin_notices`</SwmToken> hook, which is triggered when the admin screen is displayed.

```hack
<?php
/**
 * @package Hello_Dolly
 * @version 1.7.2
 */
/*
Plugin Name: Hello Dolly
Plugin URI: http://wordpress.org/plugins/hello-dolly/
Description: This is not just a plugin, it symbolizes the hope and enthusiasm of an entire generation summed up in two words sung most famously by Louis Armstrong: Hello, Dolly. When activated you will randomly see a lyric from <cite>Hello, Dolly</cite> in the upper right of your admin screen on every page.
Author: Matt Mullenweg
Version: 1.7.2
Author URI: http://ma.tt/
*/

function hello_dolly_get_lyric() {
	/** These are the lyrics to Hello Dolly */
	$lyrics = "Hello, Dolly
Well, hello, Dolly
It's so nice to have you back where you belong
You're lookin' swell, Dolly
I can tell, Dolly
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet-rest-api.php" line="3">

---

# Akismet Plugin

The 'Akismet' plugin is another example of a content plugin. It provides a REST API for interacting with the Akismet service, which helps protect the website from spam. The plugin registers several routes with the <SwmToken path="/wp-content/plugins/hello.php" pos="8:7:7" line-data="Plugin URI: http://wordpress.org/plugins/hello-dolly/">`wordpress`</SwmToken> REST API, each of which corresponds to a different function of the Akismet service.

```hack
class Akismet_REST_API {
	/**
	 * Register the REST API routes.
	 */
	public static function init() {
		if ( ! function_exists( 'register_rest_route' ) ) {
			// The REST API wasn't integrated into core until 4.4, and we support 4.0+ (for now).
			return false;
		}

		register_rest_route( 'akismet/v1', '/key', array(
			array(
				'methods' => WP_REST_Server::READABLE,
				'permission_callback' => array( 'Akismet_REST_API', 'privileged_permission_callback' ),
				'callback' => array( 'Akismet_REST_API', 'get_key' ),
			), array(
				'methods' => WP_REST_Server::EDITABLE,
				'permission_callback' => array( 'Akismet_REST_API', 'privileged_permission_callback' ),
				'callback' => array( 'Akismet_REST_API', 'set_key' ),
				'args' => array(
					'key' => array(
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet-admin.php" line="1284">

---

# Modifying Plugin Descriptions

This function in the Akismet plugin modifies the description of the plugin that is displayed in the <SwmToken path="/wp-content/plugins/hello.php" pos="8:7:7" line-data="Plugin URI: http://wordpress.org/plugins/hello-dolly/">`wordpress`</SwmToken> admin panel. This is an example of how a plugin can modify the <SwmToken path="/wp-content/plugins/hello.php" pos="8:7:7" line-data="Plugin URI: http://wordpress.org/plugins/hello-dolly/">`wordpress`</SwmToken> admin interface.

```hack
	/**
	 * When Akismet is active, remove the "Activate Akismet" step from the plugin description.
	 */
	public static function modify_plugin_description( $all_plugins ) {
		if ( isset( $all_plugins['akismet/akismet.php'] ) ) {
			if ( Akismet::get_api_key() ) {
				$all_plugins['akismet/akismet.php']['Description'] = __( 'Used by millions, Akismet is quite possibly the best way in the world to <strong>protect your blog from spam</strong>. Your site is fully configured and being protected, even while you sleep.', 'akismet' );
			}
			else {
				$all_plugins['akismet/akismet.php']['Description'] = __( 'Used by millions, Akismet is quite possibly the best way in the world to <strong>protect your blog from spam</strong>. It keeps your site protected even while you sleep. To get started, just go to <a href="admin.php?page=akismet-key-config">your Akismet Settings page</a> to set up your API key.', 'akismet' );
			}
		}

		return $all_plugins;
	}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
