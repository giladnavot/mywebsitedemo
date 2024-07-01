---
title: Exploring the Hello Dolly Plugin
---
The Hello Dolly plugin is a symbolic representation of the hope and enthusiasm of an entire generation, encapsulated in the famous song by Louis Armstrong, 'Hello, Dolly'. When activated, this plugin displays a random lyric from the song in the upper right of your admin screen on every page. It's a fun and nostalgic addition to the WordPress admin interface.

<SwmSnippet path="/wp-content/plugins/hello.php" line="1">

---

## Hello Dolly Plugin Code

This is the header of the Hello Dolly plugin. It provides basic information about the plugin such as its name, version, and a brief description of what it does.

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

<SwmSnippet path="/wp-content/plugins/hello.php" line="15">

---

## Displaying Lyrics

This part of the code defines the `hello_dolly_get_lyric` function. This function contains the lyrics to 'Hello, Dolly', splits them into separate lines, and then randomly selects a line to display.

```hack
function hello_dolly_get_lyric() {
	/** These are the lyrics to Hello Dolly */
	$lyrics = "Hello, Dolly
Well, hello, Dolly
It's so nice to have you back where you belong
You're lookin' swell, Dolly
I can tell, Dolly
You're still glowin', you're still crowin'
You're still goin' strong
I feel the room swayin'
While the band's playin'
One of our old favorite songs from way back when
So, take her wrap, fellas
Dolly, never go away again
Hello, Dolly
Well, hello, Dolly
It's so nice to have you back where you belong
You're lookin' swell, Dolly
I can tell, Dolly
You're still glowin', you're still crowin'
You're still goin' strong
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/hello.php" line="68">

---

## Activating the Plugin

This part of the code sets up the `hello_dolly` function to execute when the `admin_notices` action is called. This is how the plugin is activated and starts displaying lyrics on the admin screen.

```hack
// Now we set that function up to execute when the admin_notices action is called.
add_action( 'admin_notices', 'hello_dolly' );

```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/hello.php" line="72">

---

## Styling the Display

This part of the code defines the `dolly_css` function, which adds some CSS to position the displayed lyric on the admin screen. This function is set up to execute when the `admin_head` action is called.

```hack
function dolly_css() {
	echo "
	<style type='text/css'>
	#dolly {
		float: right;
		padding: 5px 10px;
		margin: 0;
		font-size: 12px;
		line-height: 1.6666;
	}
	.rtl #dolly {
		float: left;
	}
	.block-editor-page #dolly {
		display: none;
	}
	@media screen and (max-width: 782px) {
		#dolly,
		.rtl #dolly {
			float: none;
			padding-left: 0;
```

---

</SwmSnippet>

# Hello Dolly Plugin Functions

Hello Dolly Plugin Functions

<SwmSnippet path="/wp-content/plugins/hello.php" line="15">

---

## hello_dolly_get_lyric

The `hello_dolly_get_lyric` function is responsible for generating the lyrics. It contains a string of lyrics from the song 'Hello, Dolly', which it then splits into individual lines. It then randomly selects one of these lines to display.

```hack
function hello_dolly_get_lyric() {
	/** These are the lyrics to Hello Dolly */
	$lyrics = "Hello, Dolly
Well, hello, Dolly
It's so nice to have you back where you belong
You're lookin' swell, Dolly
I can tell, Dolly
You're still glowin', you're still crowin'
You're still goin' strong
I feel the room swayin'
While the band's playin'
One of our old favorite songs from way back when
So, take her wrap, fellas
Dolly, never go away again
Hello, Dolly
Well, hello, Dolly
It's so nice to have you back where you belong
You're lookin' swell, Dolly
I can tell, Dolly
You're still glowin', you're still crowin'
You're still goin' strong
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/hello.php" line="53">

---

## hello_dolly

The `hello_dolly` function is responsible for displaying the chosen lyric on the admin screen. It calls the `hello_dolly_get_lyric` function to get a lyric, and then displays this lyric in a paragraph element with the id 'dolly'.

```hack
function hello_dolly() {
	$chosen = hello_dolly_get_lyric();
	$lang   = '';
	if ( 'en_' !== substr( get_user_locale(), 0, 3 ) ) {
		$lang = ' lang="en"';
	}

	printf(
		'<p id="dolly"><span class="screen-reader-text">%s </span><span dir="ltr"%s>%s</span></p>',
		__( 'Quote from Hello Dolly song, by Jerry Herman:' ),
		$lang,
		$chosen
	);
}
```

---

</SwmSnippet>

<SwmSnippet path="/wp-content/plugins/hello.php" line="72">

---

## dolly_css

The `dolly_css` function is responsible for styling the paragraph element that displays the lyric. It sets the position, padding, margin, font size, and line height of the paragraph element.

```hack
function dolly_css() {
	echo "
	<style type='text/css'>
	#dolly {
		float: right;
		padding: 5px 10px;
		margin: 0;
		font-size: 12px;
		line-height: 1.6666;
	}
	.rtl #dolly {
		float: left;
	}
	.block-editor-page #dolly {
		display: none;
	}
	@media screen and (max-width: 782px) {
		#dolly,
		.rtl #dolly {
			float: none;
			padding-left: 0;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
