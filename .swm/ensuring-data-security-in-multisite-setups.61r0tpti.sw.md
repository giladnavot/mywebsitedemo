---
title: Ensuring Data Security in Multisite Setups
---
This document will cover the process of ensuring data security in a multisite setup in WordPress. We'll cover:

1. The role of the WP_Site and WP_Network classes
2. The use of the is_multisite function
3. The use of the get_locale function

<SwmSnippet path="/wp-includes/class-wp-site.php" line="2">

---

# WP_Site and WP_Network classes

The WP_Site class is used for interacting with a multisite site. It is used during load to populate the `$current_blog` global and setup the current site.

```hack
/**
 * Site API: WP_Site class
 *
 * @package WordPress
 * @subpackage Multisite
 * @since 4.5.0
 */

/**
 * Core class used for interacting with a multisite site.
 *
 * This class is used during load to populate the `$current_blog` global and
 * setup the current site.
 *
 * @since 4.5.0
 *
 * @property int    $id
 * @property int    $network_id
 * @property string $blogname
 * @property string $siteurl
 * @property int    $post_count
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/class-wp-network.php" line="2">

---

The WP_Network class is used for interacting with a multisite network. This class is most useful in WordPress multi-network installations where the ability to interact with any network of sites is required.

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

<SwmSnippet path="/wp-includes/load.php" line="1410">

---

# is_multisite function

The is_multisite function determines whether Multisite is enabled. It checks if the MULTISITE constant is defined or if the SUBDOMAIN_INSTALL, VHOST, or SUNRISE constants are defined.

```hack
function is_multisite() {
	if ( defined( 'MULTISITE' ) ) {
		return MULTISITE;
	}

	if ( defined( 'SUBDOMAIN_INSTALL' ) || defined( 'VHOST' ) || defined( 'SUNRISE' ) ) {
		return true;
	}

	return false;
}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/l10n.php" line="30">

---

# get_locale function

The get_locale function retrieves the current locale. If the locale is not set already, then the WPLANG constant is used if it is defined. If multisite, it checks options.

```hack
function get_locale() {
	global $locale, $wp_local_package;

	if ( isset( $locale ) ) {
		/** This filter is documented in wp-includes/l10n.php */
		return apply_filters( 'locale', $locale );
	}

	if ( isset( $wp_local_package ) ) {
		$locale = $wp_local_package;
	}

	// WPLANG was defined in wp-config.
	if ( defined( 'WPLANG' ) ) {
		$locale = WPLANG;
	}

	// If multisite, check options.
	if ( is_multisite() ) {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
