---
title: Overview of Site Management
---
Site Management in this repository refers to the functionality that allows administrators to control and manage various aspects of their WordPress sites. This includes actions such as activating and deactivating sites, archiving sites, and managing site users, themes, settings, and information. These actions are primarily handled in the `wp-admin/network/sites.php` file and related files in the `wp-admin/network/` directory.

The `site_id` variable is used to uniquely identify each site in the network. The `get_site` function is used to retrieve the details of a site, given its `site_id`. The `site` variable holds the details of a site, including its domain and path.

The `manage_actions` array in `wp-admin/network/sites.php` defines the messages associated with various site management actions. For example, when a site is activated, the message 'Site activated.' is displayed.

The `wp-admin/network/` directory contains several PHP files, each responsible for a specific aspect of site management. For example, `site-users.php` is used for managing site users, `site-themes.php` for managing site themes, and so on.

<SwmSnippet path="/wp-admin/network/sites.php" line="63">

---

# Site Actions

The 'manage_actions' array defines the various actions that can be performed on the site, such as activating the site. Each action is associated with a message for confirmation output.

```hack
	// A list of valid actions and their associated messaging for confirmation output.
	$manage_actions = array(
		/* translators: %s: Site URL. */
		'activateblog'   => __( 'You are about to activate the site %s.' ),
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/network/sites.php" line="161">

---

# Site Details

The 'get_site' function is used to retrieve the details of a site. The returned 'site' object contains various properties of the site, such as its domain and path.

```hack
				if ( ! current_user_can( 'delete_site', $site_id ) ) {
					$site         = get_site( $site_id );
					$site_address = untrailingslashit( $site->domain . $site->path );
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/network/site-users.php" line="200">

---

# Site Management Files

The 'sites.php' file serves as the parent file for various site-related actions. It is referenced in various other files, such as 'site-users.php', 'site-info.php', 'site-new.php', 'site-settings.php', and 'site-themes.php'.

```hack
$title = sprintf( __( 'Edit Site: %s' ), esc_html( $details->blogname ) );

$parent_file  = 'sites.php';
$submenu_file = 'sites.php';
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
