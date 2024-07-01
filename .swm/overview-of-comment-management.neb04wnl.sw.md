---
title: Overview of Comment Management
---
Comment Management refers to the functionality that allows administrators to moderate, edit, approve, trash, or delete comments on the website. This is crucial for maintaining the quality of the site's content and ensuring a respectful and productive discussion environment. The system also supports actions on multiple comments at once, which can be particularly useful for managing large volumes of comments.

<SwmSnippet path="/wp-admin/comment.php" line="21">

---

# Comment Actions

This section of the code handles the different actions that can be performed on a comment. Depending on the action received from the <SwmToken path="/wp-admin/comment.php" pos="21:7:8" line-data="if ( isset( $_POST[&#39;deletecomment&#39;] ) ) {">`$_POST`</SwmToken> or <SwmToken path="/wp-admin/comment.php" pos="31:7:8" line-data="if ( isset( $_GET[&#39;dt&#39;] ) ) {">`$_GET`</SwmToken> request, the <SwmToken path="/wp-admin/comment.php" pos="22:1:2" line-data="	$action = &#39;deletecomment&#39;;">`$action`</SwmToken> variable is set accordingly.

```hack
if ( isset( $_POST['deletecomment'] ) ) {
	$action = 'deletecomment';
}

if ( 'cdc' === $action ) {
	$action = 'delete';
} elseif ( 'mac' === $action ) {
	$action = 'approve';
}

if ( isset( $_GET['dt'] ) ) {
	if ( 'spam' === $_GET['dt'] ) {
		$action = 'spam';
	} elseif ( 'trash' === $_GET['dt'] ) {
		$action = 'trash';
	}
}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/comment.php" line="39">

---

# Comment Retrieval

Here, the comment ID is retrieved from the request and used to fetch the corresponding comment. If the comment is associated with a trashed post, an error message is displayed.

```hack
if ( isset( $_REQUEST['c'] ) ) {
	$comment_id = absint( $_REQUEST['c'] );
	$comment    = get_comment( $comment_id );

	// Prevent actions on a comment associated with a trashed post.
	if ( $comment && 'trash' === get_post_status( $comment->comment_post_ID ) ) {
		wp_die(
			__( 'You cannot edit this comment because the associated post is in the Trash. Please restore the post first, then try again.' )
		);
	}
} else {
	$comment = null;
}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/comment.php" line="53">

---

# Comment Editing and Moderation

This part of the code handles the 'editcomment' action. It checks if the user has the necessary permissions to edit the comment and if the comment is not already trashed. If these conditions are met, the comment is retrieved for editing.

```hack
switch ( $action ) {

	case 'editcomment':
		// Used in the HTML title tag.
		$title = __( 'Edit Comment' );

		get_current_screen()->add_help_tab(
			array(
				'id'      => 'overview',
				'title'   => __( 'Overview' ),
				'content' =>
					'<p>' . __( 'You can edit the information left in a comment if needed. This is often useful when you notice that a commenter has made a typographical error.' ) . '</p>' .
					'<p>' . __( 'You can also moderate the comment from this screen using the Status box, where you can also change the timestamp of the comment.' ) . '</p>',
			)
		);

		get_current_screen()->set_help_sidebar(
			'<p><strong>' . __( 'For more information:' ) . '</strong></p>' .
			'<p>' . __( '<a href="https://wordpress.org/documentation/article/comments-screen/">Documentation on Comments</a>' ) . '</p>' .
			'<p>' . __( '<a href="https://wordpress.org/support/forums/">Support forums</a>' ) . '</p>'
		);
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/comment.php" line="96">

---

# Comment Deletion, Approval, Trashing, and Spamming

This section handles the 'delete', 'approve', 'trash', and 'spam' actions. Similar to the editing process, it checks for the necessary permissions and the comment status before proceeding.

```hack
	case 'delete':
	case 'approve':
	case 'trash':
	case 'spam':
		// Used in the HTML title tag.
		$title = __( 'Moderate Comment' );

		if ( ! $comment ) {
			wp_redirect( admin_url( 'edit-comments.php?error=1' ) );
			die();
		}

		if ( ! current_user_can( 'edit_comment', $comment->comment_ID ) ) {
			wp_redirect( admin_url( 'edit-comments.php?error=2' ) );
			die();
		}

		// No need to re-approve/re-trash/re-spam a comment.
		if ( str_replace( '1', 'approve', $comment->comment_approved ) === $action ) {
			wp_redirect( admin_url( 'edit-comments.php?same=' . $comment_id ) );
			die();
```

---

</SwmSnippet>

<SwmSnippet path="/wp-admin/edit-comments.php" line="9">

---

# Comment List Management

This file is responsible for managing the list of comments displayed in the <SwmToken path="/wp-admin/edit-comments.php" pos="9:2:2" line-data="/** WordPress Administration Bootstrap */">`WordPress`</SwmToken> admin panel. It handles bulk actions on comments and updates the comment counts for different statuses.

```hack
/** WordPress Administration Bootstrap */
require_once __DIR__ . '/admin.php';
if ( ! current_user_can( 'edit_posts' ) ) {
	wp_die(
		'<h1>' . __( 'You need a higher level of permission.' ) . '</h1>' .
		'<p>' . __( 'Sorry, you are not allowed to edit comments.' ) . '</p>',
		403
	);
}

$wp_list_table = _get_list_table( 'WP_Comments_List_Table' );
$pagenum       = $wp_list_table->get_pagenum();

$doaction = $wp_list_table->current_action();

if ( $doaction ) {
	check_admin_referer( 'bulk-comments' );

	if ( 'delete_all' === $doaction && ! empty( $_REQUEST['pagegen_timestamp'] ) ) {
		/**
		 * @global wpdb $wpdb WordPress database abstraction object.
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
