---
title: Introduction to Post Management
---
Post Management in mywebsitedemo refers to the functionality of handling WordPress posts. It involves creating, editing, and deleting posts. This is primarily handled in the `wp-admin` directory, specifically within the `post.php` and `post-new.php` files. The `post_type` variable is used to determine the type of the post, while the `post_ID` and `post_id` variables are used to uniquely identify each post. The `parent_file` variable is used to navigate within the post management interface.

<SwmSnippet path="/wp-admin/post-new.php" line="20">

---

## Post Creation

Here, a new post is being created. The `post_type` is set to 'post' by default, but can be changed if other post types are defined in the system.

```hack
	$post_type = 'post';
} elseif ( in_array( $_GET['post_type'], get_post_types( array( 'show_ui' => true ) ), true ) ) {
	$post_type = $_GET['post_type'];
} else {
	wp_die( __( 'Invalid post type.' ) );
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/post.php" line="37">

---

## Post Editing

In this section, an existing post is being fetched for editing. The `post_id` is used to retrieve the specific post from the database.

```hack
if ( $post_id ) {
	$post = get_post( $post_id );
}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/post.php" line="151">

---

## Post Deletion

This section checks the `post_type`. If it's a 'post', it sets the `parent_file` to 'edit.php', which is the file responsible for displaying the post editing interface, including the option to delete the post.

```hack
		}

		$post_type = $post->post_type;
		if ( 'post' === $post_type ) {
			$parent_file   = 'edit.php';
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
