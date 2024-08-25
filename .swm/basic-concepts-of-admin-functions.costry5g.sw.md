---
title: Basic Concepts of Admin Functions
---
Admin Functions in the WordPress project are a set of functionalities that provide the ability to manage the website. They are primarily located in the `wp-admin` directory. These functions include managing users, posts, comments, and other site settings. The `admin.php` file is the main entry point for these functions. It sets up the environment and loads the necessary resources for the admin interface. The `admin-functions.php` file, however, is deprecated and its functionalities have been moved to `wp-admin/includes/admin.php`. The admin interface also includes styles and scripts for the admin menu and other UI elements, defined in `wp-admin/css/colors/_admin.scss` and other CSS files.

<SwmSnippet path="/wp-admin/admin.php" line="1">

---

# Admin Functions in wp-admin/admin.php

This file is the bootstrap for the WordPress admin. It sets up the admin environment and loads the necessary files and functions. It also defines several constants that are used in the admin interface.

```hack
<?php
/**
 * WordPress Administration Bootstrap
 *
 * @package WordPress
 * @subpackage Administration
 */

/**
 * In WordPress Administration Screens
 *
 * @since 2.3.2
 */
if ( ! defined( 'WP_ADMIN' ) ) {
	define( 'WP_ADMIN', true );
}

if ( ! defined( 'WP_NETWORK_ADMIN' ) ) {
	define( 'WP_NETWORK_ADMIN', false );
}

```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/includes/deprecated.php" line="26">

---

# Deprecated Admin Functions

This file contains deprecated admin functions. These functions were used in previous versions of WordPress but are no longer used. They are kept for backward compatibility.

```hack
/**
 * Unused Admin function.
 *
 * @since 2.0.0
 * @deprecated 2.5.0
 *
 */
function documentation_link() {
	_deprecated_function( __FUNCTION__, '2.5.0' );
}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/admin-ajax.php" line="1">

---

# Admin Functions in wp-admin/admin-ajax.php

This file handles Ajax requests in the WordPress admin. 

```hack
<?php
/**
 * WordPress Ajax Process Execution
 *
 * @package WordPress
 * @subpackage Administration
 *
 * @link https://codex.wordpress.org/AJAX_in_Plugins
 */

/**
 * Executing Ajax process.
 *
 * @since 2.1.0
 */
define( 'DOING_AJAX', true );
if ( ! defined( 'WP_ADMIN' ) ) {
	define( 'WP_ADMIN', true );
}

/** Load WordPress Bootstrap */
```

---

</SwmSnippet>



&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
