---
title: Introduction to Akismet Plugin
---
The Akismet Plugin is a powerful <SwmToken path="/wp-content/plugins/akismet/class.akismet-admin.php" pos="88:31:33" line-data="				__( &#39;We collect information about visitors who comment on Sites that use our Akismet Anti-spam service. The information we collect depends on how the User sets up Akismet for the Site, but typically includes the commenter\&#39;s IP address, user agent, referrer, and Site URL (along with other information directly provided by the commenter such as their name, username, email address, and the comment itself).&#39;, &#39;akismet&#39; )">`Anti-spam`</SwmToken> plugin used in this <SwmToken path="/wp-content/plugins/akismet/class.akismet.php" pos="1627:25:25" line-data="			$message = &#39;&lt;strong&gt;&#39;.sprintf(esc_html__( &#39;Akismet %s requires WordPress %s or higher.&#39; , &#39;akismet&#39;), AKISMET_VERSION, AKISMET__MINIMUM_WP_VERSION ).&#39;&lt;/strong&gt; &#39;.sprintf(__(&#39;Please &lt;a href=&quot;%1$s&quot;&gt;upgrade WordPress&lt;/a&gt; to a current version, or &lt;a href=&quot;%2$s&quot;&gt;downgrade to version 2.4 of the Akismet plugin&lt;/a&gt;.&#39;, &#39;akismet&#39;), &#39;https://codex.wordpress.org/Upgrading_WordPress&#39;, &#39;https://wordpress.org/extend/plugins/akismet/download/&#39;);">`WordPress`</SwmToken> project. It is designed to protect the website from spam, keeping the site secure even when you're not actively managing it. The plugin works by filtering and checking comments against the Akismet web service to see if they look like spam or not, thereby preventing harmful content from being published on the site.

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet.php" line="1623">

---

## Activating the Akismet Plugin

This is the <SwmToken path="/wp-content/plugins/akismet/class.akismet.php" pos="1623:7:7" line-data="	public static function plugin_activation() {">`plugin_activation`</SwmToken> function. It is used to activate the Akismet Plugin. It checks the <SwmToken path="/wp-content/plugins/akismet/class.akismet.php" pos="1627:25:25" line-data="			$message = &#39;&lt;strong&gt;&#39;.sprintf(esc_html__( &#39;Akismet %s requires WordPress %s or higher.&#39; , &#39;akismet&#39;), AKISMET_VERSION, AKISMET__MINIMUM_WP_VERSION ).&#39;&lt;/strong&gt; &#39;.sprintf(__(&#39;Please &lt;a href=&quot;%1$s&quot;&gt;upgrade WordPress&lt;/a&gt; to a current version, or &lt;a href=&quot;%2$s&quot;&gt;downgrade to version 2.4 of the Akismet plugin&lt;/a&gt;.&#39;, &#39;akismet&#39;), &#39;https://codex.wordpress.org/Upgrading_WordPress&#39;, &#39;https://wordpress.org/extend/plugins/akismet/download/&#39;);">`WordPress`</SwmToken> version and if it is compatible, the plugin is activated.

```hack
	public static function plugin_activation() {
		if ( version_compare( $GLOBALS['wp_version'], AKISMET__MINIMUM_WP_VERSION, '<' ) ) {
			load_plugin_textdomain( 'akismet' );
			
			$message = '<strong>'.sprintf(esc_html__( 'Akismet %s requires WordPress %s or higher.' , 'akismet'), AKISMET_VERSION, AKISMET__MINIMUM_WP_VERSION ).'</strong> '.sprintf(__('Please <a href="%1$s">upgrade WordPress</a> to a current version, or <a href="%2$s">downgrade to version 2.4 of the Akismet plugin</a>.', 'akismet'), 'https://codex.wordpress.org/Upgrading_WordPress', 'https://wordpress.org/extend/plugins/akismet/download/');

			Akismet::bail_on_activation( $message );
		} elseif ( ! empty( $_SERVER['SCRIPT_NAME'] ) && false !== strpos( $_SERVER['SCRIPT_NAME'], '/wp-admin/plugins.php' ) ) {
			add_option( 'Activated_Akismet', true );
		}
	}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet.php" line="1635">

---

## Deactivating the Akismet Plugin

This is the <SwmToken path="/wp-content/plugins/akismet/class.akismet.php" pos="1639:7:7" line-data="	public static function plugin_deactivation( ) {">`plugin_deactivation`</SwmToken> function. It is used to deactivate the Akismet Plugin. It removes all connection options and scheduled cron jobs related to the plugin.

```hack
	/**
	 * Removes all connection options
	 * @static
	 */
	public static function plugin_deactivation( ) {
		self::deactivate_key( self::get_api_key() );
		
		// Remove any scheduled cron jobs.
		$akismet_cron_events = array(
			'akismet_schedule_cron_recheck',
			'akismet_scheduled_delete',
		);
		
		foreach ( $akismet_cron_events as $akismet_cron_event ) {
			$timestamp = wp_next_scheduled( $akismet_cron_event );
			
			if ( $timestamp ) {
				wp_unschedule_event( $timestamp, $akismet_cron_event );
			}
		}
	}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/_inc/akismet-admin.css" line="1">

---

## Akismet Plugin's CSS Styling

This is the CSS styling for the Akismet Plugin. It sets the background color and font family for the plugin container.

```css
#akismet-plugin-container {
	background-color: var(--akismet-color-light-grey);
	font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen-Sans', 'Ubuntu', 'Cantarell', 'Helvetica Neue', sans-serif;
    --akismet-color-charcoal: #272635;
	--akismet-color-light-grey: #f6f7f7;
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/_inc/akismet.js" line="1">

---

## Akismet Plugin's <SwmToken path="/wp-includes/SimplePie/Enclosure.php" pos="138:4:4" line-data="	var $javascript;">`javascript`</SwmToken> Functionality

This is the <SwmToken path="/wp-includes/SimplePie/Enclosure.php" pos="138:4:4" line-data="	var $javascript;">`javascript`</SwmToken> file for the Akismet Plugin. It contains various functions that add interactivity to the plugin, such as handling mouseover events and AJAX requests.

```javascript
jQuery( function ( $ ) {
	var mshotRemovalTimer = null;
	var mshotRetryTimer = null;
	var mshotTries = 0;
	var mshotRetryInterval = 1000;
	var mshotEnabledLinkSelector = 'a[id^="author_comment_url"], tr.pingback td.column-author a:first-of-type, td.comment p a';

	var preloadedMshotURLs = [];

	$('.akismet-status').each(function () {
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet-admin.php" line="1284">

---

## Modifying the Akismet Plugin Description

This function <SwmToken path="/wp-content/plugins/akismet/class.akismet-admin.php" pos="1287:7:7" line-data="	public static function modify_plugin_description( $all_plugins ) {">`modify_plugin_description`</SwmToken> is used to modify the description of the Akismet Plugin based on whether it is activated or not.

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

# Akismet Plugin Functions

This section provides an overview of the key functions of the Akismet Plugin.

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet-rest-api.php" line="150">

---

## Akismet API Key Management

These lines of code define functions for getting, setting, and deleting the Akismet API key. The API key is crucial for authenticating requests to the Akismet API.

```hack
	public static function get_key( $request = null ) {
		return rest_ensure_response( Akismet::get_api_key() );
	}

	/**
	 * Set the API key, if possible.
	 *
	 * @param WP_REST_Request $request
	 * @return WP_Error|WP_REST_Response
	 */
	public static function set_key( $request ) {
		if ( defined( 'WPCOM_API_KEY' ) ) {
			return rest_ensure_response( new WP_Error( 'hardcoded_key', __( 'This site\'s API key is hardcoded and cannot be changed via the API.', 'akismet' ), array( 'status'=> 409 ) ) );
		}

		$new_api_key = $request->get_param( 'key' );

		if ( ! self::key_is_valid( $new_api_key ) ) {
			return rest_ensure_response( new WP_Error( 'invalid_key', __( 'The value provided is not a valid and registered API key.', 'akismet' ), array( 'status' => 400 ) ) );
		}

```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet-cli.php" line="25">

---

## Checking Comments for Spam

This function checks one or more comments against the Akismet API to determine if they are spam. It can either change the status of the comment based on the result or simply report the result without changing the status.

```hack
	public function check( $args, $assoc_args ) {
		foreach ( $args as $comment_id ) {
			if ( isset( $assoc_args['noaction'] ) ) {
				// Check the comment, but don't reclassify it.
				$api_response = Akismet::check_db_comment( $comment_id, 'wp-cli' );
			}
			else {
				$api_response = Akismet::recheck_comment( $comment_id, 'wp-cli' );
			}
			
			if ( 'true' === $api_response ) {
				WP_CLI::line( sprintf( __( "Comment #%d is spam.", 'akismet' ), $comment_id ) );
			}
			else if ( 'false' === $api_response ) {
				WP_CLI::line( sprintf( __( "Comment #%d is not spam.", 'akismet' ), $comment_id ) );
			}
			else {
				if ( false === $api_response ) {
					WP_CLI::error( __( "Failed to connect to Akismet.", 'akismet' ) );
				}
				else if ( is_wp_error( $api_response ) ) {
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet-rest-api.php" line="198">

---

## Managing Akismet Settings

These functions are used to get and set the Akismet settings. The settings include options such as whether to automatically check all comments for spam and whether to discard the worst spam.

```hack
	public static function get_settings( $request = null ) {
		return rest_ensure_response( array(
			'akismet_strictness' => ( get_option( 'akismet_strictness', '1' ) === '1' ),
			'akismet_show_user_comments_approved' => ( get_option( 'akismet_show_user_comments_approved', '1' ) === '1' ),
		) );
	}

	/**
	 * Update the Akismet settings.
	 *
	 * @param WP_REST_Request $request
	 * @return WP_Error|WP_REST_Response
	 */
	public static function set_boolean_settings( $request ) {
		foreach ( array(
			'akismet_strictness',
			'akismet_show_user_comments_approved',
		) as $setting_key ) {

			$setting_value = $request->get_param( $setting_key );
			if ( is_null( $setting_value ) ) {
```

---

</SwmSnippet>

# Akismet Plugin Endpoints

Akismet Plugin Endpoints

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet-rest-api.php" line="150">

---

## /akismet/v1/key Endpoint

The `/akismet/v1/key` endpoint is used to get the current Akismet API key. It's a GET request that doesn't require any parameters and returns the API key in the response.

```hack
	public static function get_key( $request = null ) {
		return rest_ensure_response( Akismet::get_api_key() );
	}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/akismet/class.akismet-rest-api.php" line="270">

---

## /akismet/v1/stats Endpoint

The `/akismet/v1/stats` endpoint is used to get the Akismet stats for a given time period. It's a GET request that requires the 'interval' parameter, which can be 'all', <SwmToken path="/wp-content/plugins/akismet/class.akismet-rest-api.php" pos="71:31:33" line-data="					&#39;description&#39; =&gt; __( &#39;The time period for which to retrieve stats. Options: 60-days, 6-months, all&#39;, &#39;akismet&#39; ),">`60-days`</SwmToken>, or <SwmToken path="/wp-content/plugins/akismet/class.akismet-admin.php" pos="888:8:10" line-data="		foreach( array( &#39;6-months&#39;, &#39;all&#39; ) as $interval ) {">`6-months`</SwmToken>. The response includes the spam and ham counts, as well as the accuracy of the spam detection for the specified interval.

```hack
	public static function get_stats( $request ) {
		$api_key = Akismet::get_api_key();

		$interval = $request->get_param( 'interval' );

		$stat_totals = array();

		$request_args = array(
			'blog' => get_option( 'home' ),
			'key' => $api_key,
			'from' => $interval,
		);

		$request_args = apply_filters( 'akismet_request_args', $request_args, 'get-stats' );

		$response = Akismet::http_post( Akismet::build_query( $request_args ), 'get-stats' );

		if ( ! empty( $response[1] ) ) {
			$stat_totals[$interval] = json_decode( $response[1] );
		}

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
