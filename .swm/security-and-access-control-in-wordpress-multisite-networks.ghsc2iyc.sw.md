---
title: Security and Access control in WordPress Multisite Networks
---
This document will cover the process of ensuring security and access control in a WordPress multisite network. We'll cover:

1. The role of the WP_Http class
2. The function of the WP_Network_Query class
3. The purpose of the WP_Network class
4. The use of the wp_should_upgrade_global_tables function
5. The function of the is_protected_endpoint function
6. The role of the populate_network_meta function
7. The use of the get_plugin_data function
8. The function of the wpdb class

<SwmSnippet path="/wp-includes/class-wp-http.php" line="17">

---

# The role of the WP_Http class

The WP_Http class is used for managing HTTP transports and making HTTP requests. It is used to make outgoing HTTP requests easy for developers while still being compatible with the many PHP configurations under which WordPress runs.

```hack
/**
 * Core class used for managing HTTP transports and making HTTP requests.
 *
 * This class is used to consistently make outgoing HTTP requests easy for developers
 * while still being compatible with the many PHP configurations under which
 * WordPress runs.
 *
 * Debugging includes several actions, which pass different variables for debugging the HTTP API.
 *
 * @since 2.7.0
 */
#[AllowDynamicProperties]
class WP_Http {

	// Aliases for HTTP response codes.
	const HTTP_CONTINUE       = 100;
	const SWITCHING_PROTOCOLS = 101;
	const PROCESSING          = 102;
	const EARLY_HINTS         = 103;

	const OK                            = 200;
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/class-wp-network-query.php" line="2">

---

# The function of the WP_Network_Query class

The WP_Network_Query class is used for querying networks. It provides a way to retrieve network data from the database using the most efficient queries possible.

```hack
/**
 * Network API: WP_Network_Query class
 *
 * @package WordPress
 * @subpackage Multisite
 * @since 4.6.0
 */

/**
 * Core class used for querying networks.
 *
 * @since 4.6.0
 *
 * @see WP_Network_Query::__construct() for accepted arguments.
 */
#[AllowDynamicProperties]
class WP_Network_Query {

	/**
	 * SQL for database query.
	 *
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/class-wp-network.php" line="2">

---

# The purpose of the WP_Network class

The WP_Network class is used for interacting with a multisite network. It is used during load to populate the `$current_site` global and setup the current network.

```hack
/**
 * Network API: WP_Network class
 *
 * @package WordPress
 * @subpackage Multisite
 * @since 4.4.0
 */

/**
 * Core class used for interacting with a multisite network.
 *
 * This class is used during load to populate the `$current_site` global and
 * setup the current network.
 *
 * This class is most useful in WordPress multi-network installations where the
 * ability to interact with any network of sites is required.
 *
 * @since 4.4.0
 *
 * @property int $id
 * @property int $site_id
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/includes/upgrade.php" line="3654">

---

# The use of the wp_should_upgrade_global_tables function

The wp_should_upgrade_global_tables function performs a series of checks to ensure the environment allows for the safe upgrading of global WordPress database tables. It is necessary because global tables will commonly grow to millions of rows on large installations, and the ability to control their upgrade routines can be critical to the operation of large networks.

```hack
/**
 * Determine if global tables should be upgraded.
 *
 * This function performs a series of checks to ensure the environment allows
 * for the safe upgrading of global WordPress database tables. It is necessary
 * because global tables will commonly grow to millions of rows on large
 * installations, and the ability to control their upgrade routines can be
 * critical to the operation of large networks.
 *
 * In a future iteration, this function may use `wp_is_large_network()` to more-
 * intelligently prevent global table upgrades. Until then, we make sure
 * WordPress is on the main site of the main network, to avoid running queries
 * more than once in multi-site or multi-network environments.
 *
 * @since 4.3.0
 *
 * @return bool Whether to run the upgrade routines on global tables.
 */
function wp_should_upgrade_global_tables() {

	// Return false early if explicitly not upgrading.
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/load.php" line="1133">

---

# The function of the is_protected_endpoint function

The is_protected_endpoint function determines whether we are currently on an endpoint that should be protected against WSODs. It protects login pages and the admin backend.

```hack
/**
 * Determines whether we are currently on an endpoint that should be protected against WSODs.
 *
 * @since 5.2.0
 *
 * @global string $pagenow The filename of the current screen.
 *
 * @return bool True if the current endpoint should be protected.
 */
function is_protected_endpoint() {
	// Protect login pages.
	if ( isset( $GLOBALS['pagenow'] ) && 'wp-login.php' === $GLOBALS['pagenow'] ) {
		return true;
	}

	// Protect the admin backend.
	if ( is_admin() && ! wp_doing_ajax() ) {
		return true;
	}

	// Protect Ajax actions that could help resolve a fatal error should be available.
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/includes/schema.php" line="1154">

---

# The role of the populate_network_meta function

The populate_network_meta function creates WordPress network meta and sets the default values. It is used when a new network is created.

```hack
/**
 * Creates WordPress network meta and sets the default values.
 *
 * @since 5.1.0
 *
 * @global wpdb $wpdb          WordPress database abstraction object.
 * @global int  $wp_db_version WordPress database version.
 *
 * @param int   $network_id Network ID to populate meta for.
 * @param array $meta       Optional. Custom meta $key => $value pairs to use. Default empty array.
 */
function populate_network_meta( $network_id, array $meta = array() ) {
	global $wpdb, $wp_db_version;

	$network_id = (int) $network_id;

	$email             = ! empty( $meta['admin_email'] ) ? $meta['admin_email'] : '';
	$subdomain_install = isset( $meta['subdomain_install'] ) ? (int) $meta['subdomain_install'] : 0;

	// If a user with the provided email does not exist, default to the current user as the new network admin.
	$site_user = ! empty( $email ) ? get_user_by( 'email', $email ) : false;
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/includes/plugin.php" line="10">

---

# The use of the get_plugin_data function

The get_plugin_data function parses the plugin contents to retrieve plugin's metadata. All plugin headers must be on their own line. Plugin description must not have any newlines, otherwise only parts of the description will be displayed.

```hack
 * Parses the plugin contents to retrieve plugin's metadata.
 *
 * All plugin headers must be on their own line. Plugin description must not have
 * any newlines, otherwise only parts of the description will be displayed.
 * The below is formatted for printing.
 *
 *     /*
 *     Plugin Name: Name of the plugin.
 *     Plugin URI: The home page of the plugin.
 *     Description: Plugin description.
 *     Author: Plugin author's name.
 *     Author URI: Link to the author's website.
 *     Version: Plugin version.
 *     Text Domain: Optional. Unique identifier, should be same as the one used in
 *          load_plugin_textdomain().
 *     Domain Path: Optional. Only useful if the translations are located in a
 *          folder above the plugin's base path. For example, if .mo files are
 *          located in the locale folder then Domain Path will be "/locale/" and
 *          must have the first slash. Defaults to the base folder the plugin is
 *          located in.
 *     Network: Optional. Specify "Network: true" to require that a plugin is activated
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/class-wpdb.php" line="39">

---

# The function of the wpdb class

The wpdb class is used to interact with a database without needing to use raw SQL statements. By default, WordPress uses this class to instantiate the global $wpdb object, providing access to the WordPress database.

```hack
/**
 * WordPress database access abstraction class.
 *
 * This class is used to interact with a database without needing to use raw SQL statements.
 * By default, WordPress uses this class to instantiate the global $wpdb object, providing
 * access to the WordPress database.
 *
 * It is possible to replace this class with your own by setting the $wpdb global variable
 * in wp-content/db.php file to your class. The wpdb class will still be included, so you can
 * extend it or simply use your own.
 *
 * @link https://developer.wordpress.org/reference/classes/wpdb/
 *
 * @since 0.71
 */
#[AllowDynamicProperties]
class wpdb {

	/**
	 * Whether to show SQL/DB errors.
	 *
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
