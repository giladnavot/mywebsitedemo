---
title: Basic Concepts of Plugin Management
---
Plugin Management in WordPress, as seen in the mywebsitedemo repository, involves the handling of plugins within the WordPress system. This includes the activation, deactivation, updating, and uninstallation of plugins. The `plugins.php` and `plugin-install.php` files in the `wp-admin` directory are primarily responsible for these tasks. They use various variables and functions to manage the state of plugins, such as `plugin_info`, `plugins`, `title`, and `have_non_network_plugins`. These variables store information about the plugins, their active state, and their network compatibility.

<SwmSnippet path="/wp-admin/plugins.php" line="307">

---

## Plugin Variables

The `plugin_info` variable is used to store information about the plugins.

```hack
				<?php

				$plugin_info              = array();
				$have_non_network_plugins = false;
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/plugins.php" line="153">

---

The `plugins` variable is used to store the list of checked plugins from the form submission.

```hack
				$plugins = (array) wp_unslash( $_POST['checked'] );
			} else {
				$plugins = array();
			}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/plugins.php" line="324">

---

The `folder_plugins` variable is used to get the list of plugins from a specific folder.

```hack
					} else {
						// Get plugins list from that folder.
						$folder_plugins = get_plugins( '/' . $plugin_slug );
						if ( $folder_plugins ) {
							foreach ( $folder_plugins as $plugin_file => $data ) {
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/plugins.php" line="620">

---

## Plugin Titles

The `title` variable is used to set the title of the HTML page for the plugins section.

```hack
// Used in the HTML title tag.
$title       = __( 'Plugins' );
$parent_file = 'plugins.php';
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/plugin-install.php" line="50">

---

The `title` variable is also used in the plugin installation page to set the title of the HTML page.

```hack
// Used in the HTML title tag.
$title       = __( 'Add Plugins' );
$parent_file = 'plugins.php';
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/network/plugins.php" line="1">

---

## Plugin Files

The `plugins.php` file is included in the network plugins administration panel to manage plugins across the network.

```hack
<?php
/**
 * Network Plugins administration panel.
 *
 * @package WordPress
 * @subpackage Multisite
 * @since 3.1.0
 */

/** Load WordPress Administration Bootstrap */
require_once __DIR__ . '/admin.php';

require ABSPATH . 'wp-admin/plugins.php';

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
