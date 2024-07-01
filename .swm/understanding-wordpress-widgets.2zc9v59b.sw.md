---
title: Understanding WordPress Widgets
---
WordPress Widgets are PHP objects that echo string data to a webpage at designated areas, or 'sidebars'. They are a way to add features or content to your site without having to know any code. Widgets can be added, removed, and rearranged in the WordPress admin under Appearance > Widgets. In the context of this repository, there are several widget classes defined, such as `WP_Widget_Text`, `WP_Widget_Pages`, `WP_Widget_Media`, `WP_Widget_Categories`, `WP_Widget_Archives`, `WP_Widget_Block`, `WP_Widget_Search`, `WP_Widget_Links`, `WP_Widget_Tag_Cloud`, `WP_Widget_RSS`, and others. Each of these classes extends the `WP_Widget` class and implements a specific type of widget functionality.

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-text.php" line="1">

---

# WP_Widget_Text

The WP_Widget_Text class is used to implement a Text widget. This widget allows users to add arbitrary text or HTML to their site. The widget can be found in the WordPress admin panel under Appearance > Widgets.

```hack
<?php
/**
 * Widget API: WP_Widget_Text class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Text widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Text extends WP_Widget {

	/**
	 * Whether or not the widget has been registered yet.
	 *
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-media.php" line="1">

---

# WP_Widget_Media

The WP_Widget_Media class is used to implement a Media widget. This widget allows users to display a media file on their site. The media can be an image, video, audio, or even a playlist.

```hack
<?php
/**
 * Widget API: WP_Media_Widget class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.8.0
 */

/**
 * Core class that implements a media widget.
 *
 * @since 4.8.0
 *
 * @see WP_Widget
 */
abstract class WP_Widget_Media extends WP_Widget {

	/**
	 * Translation labels.
	 *
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-pages.php" line="1">

---

# WP_Widget_Pages

The WP_Widget_Pages class is used to implement a Pages widget. This widget allows users to display a list of their site's pages.

```hack
<?php
/**
 * Widget API: WP_Widget_Pages class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Pages widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Pages extends WP_Widget {

	/**
	 * Sets up a new Pages widget instance.
	 *
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-archives.php" line="1">

---

# WP_Widget_Archives

The WP_Widget_Archives class is used to implement an Archives widget. This widget allows users to display a monthly archive of their site's posts.

```hack
<?php
/**
 * Widget API: WP_Widget_Archives class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement the Archives widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Archives extends WP_Widget {

	/**
	 * Sets up a new Archives widget instance.
	 *
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-links.php" line="1">

---

# WP_Widget_Links

The WP_Widget_Links class is used to implement a Links widget. This widget allows users to display a list of links (also known as a blogroll) on their site.

```hack
<?php
/**
 * Widget API: WP_Widget_Links class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Links widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Links extends WP_Widget {

	/**
	 * Sets up a new Links widget instance.
	 *
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-search.php" line="1">

---

# WP_Widget_Search

The WP_Widget_Search class is used to implement a Search widget. This widget allows users to display a search form on their site.

```hack
<?php
/**
 * Widget API: WP_Widget_Search class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Search widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Search extends WP_Widget {

	/**
	 * Sets up a new Search widget instance.
	 *
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-block.php" line="1">

---

# WP_Widget_Block

The WP_Widget_Block class is used to implement a Block widget. This widget allows users to display a single block on their site.

```hack
<?php
/**
 * Widget API: WP_Widget_Block class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 5.8.0
 */

/**
 * Core class used to implement a Block widget.
 *
 * @since 5.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Block extends WP_Widget {

	/**
	 * Default instance.
	 *
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-categories.php" line="1">

---

# WP_Widget_Categories

The WP_Widget_Categories class is used to implement a Categories widget. This widget allows users to display a list or dropdown of categories on their site.

```hack
<?php
/**
 * Widget API: WP_Widget_Categories class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Categories widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Categories extends WP_Widget {

	/**
	 * Sets up a new Categories widget instance.
	 *
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-custom-html.php" line="1">

---

# WP_Widget_Custom_HTML

The WP_Widget_Custom_HTML class is used to implement a Custom HTML widget. This widget allows users to add custom HTML to their site.

```hack
<?php
/**
 * Widget API: WP_Widget_Custom_HTML class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.8.1
 */

/**
 * Core class used to implement a Custom HTML widget.
 *
 * @since 4.8.1
 *
 * @see WP_Widget
 */
class WP_Widget_Custom_HTML extends WP_Widget {

	/**
	 * Whether or not the widget has been registered yet.
	 *
```

---

</SwmSnippet>

# WordPress Widgets

This section provides an overview of the main functions in the WordPress widgets.

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-text.php" line="2">

---

## WP_Widget_Text

The `WP_Widget_Text` class is used to implement a Text widget. It allows arbitrary text or HTML to be added to the widget areas.

```hack
/**
 * Widget API: WP_Widget_Text class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Text widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Text extends WP_Widget {

	/**
	 * Whether or not the widget has been registered yet.
	 *
	 * @since 4.8.1
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-media.php" line="2">

---

## WP_Widget_Media

The `WP_Widget_Media` class is a base class used to implement media widgets for images, audio, and video.

```hack
/**
 * Widget API: WP_Media_Widget class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.8.0
 */

/**
 * Core class that implements a media widget.
 *
 * @since 4.8.0
 *
 * @see WP_Widget
 */
abstract class WP_Widget_Media extends WP_Widget {

	/**
	 * Translation labels.
	 *
	 * @since 4.8.0
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-pages.php" line="2">

---

## WP_Widget_Pages

The `WP_Widget_Pages` class is used to implement a Pages widget. It displays a list of pages from your WordPress site.

```hack
/**
 * Widget API: WP_Widget_Pages class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Pages widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Pages extends WP_Widget {

	/**
	 * Sets up a new Pages widget instance.
	 *
	 * @since 2.8.0
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-categories.php" line="2">

---

## WP_Widget_Categories

The `WP_Widget_Categories` class is used to implement a Categories widget. It displays a list or dropdown of categories.

```hack
/**
 * Widget API: WP_Widget_Categories class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Categories widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Categories extends WP_Widget {

	/**
	 * Sets up a new Categories widget instance.
	 *
	 * @since 2.8.0
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-search.php" line="2">

---

## WP_Widget_Search

The `WP_Widget_Search` class is used to implement a Search widget. It displays a search form for your site.

```hack
/**
 * Widget API: WP_Widget_Search class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Search widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Search extends WP_Widget {

	/**
	 * Sets up a new Search widget instance.
	 *
	 * @since 2.8.0
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-links.php" line="2">

---

## WP_Widget_Links

The `WP_Widget_Links` class is used to implement a Links widget. It displays a list of links (also known as a blogroll).

```hack
/**
 * Widget API: WP_Widget_Links class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Links widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Links extends WP_Widget {

	/**
	 * Sets up a new Links widget instance.
	 *
	 * @since 2.8.0
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-recent-comments.php" line="2">

---

## WP_Widget_Recent_Comments

The `WP_Widget_Recent_Comments` class is used to implement a Recent Comments widget. It displays a list of your site's most recent comments.

```hack
/**
 * Widget API: WP_Widget_Recent_Comments class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Recent Comments widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Recent_Comments extends WP_Widget {

	/**
	 * Sets up a new Recent Comments widget instance.
	 *
	 * @since 2.8.0
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-tag-cloud.php" line="2">

---

## WP_Widget_Tag_Cloud

The `WP_Widget_Tag_Cloud` class is used to implement a Tag Cloud widget. It displays a cloud of your most used tags.

```hack
/**
 * Widget API: WP_Widget_Tag_Cloud class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Tag cloud widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Tag_Cloud extends WP_Widget {

	/**
	 * Sets up a new Tag Cloud widget instance.
	 *
	 * @since 2.8.0
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-rss.php" line="2">

---

## WP_Widget_RSS

The `WP_Widget_RSS` class is used to implement a RSS widget. It displays entries from any RSS or Atom feed.

```hack
/**
 * Widget API: WP_Widget_RSS class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a RSS widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_RSS extends WP_Widget {

	/**
	 * Sets up a new RSS widget instance.
	 *
	 * @since 2.8.0
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-calendar.php" line="2">

---

## WP_Widget_Calendar

The `WP_Widget_Calendar` class is used to implement a Calendar widget. It displays a calendar of your site's posts.

```hack
/**
 * Widget API: WP_Widget_Calendar class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement the Calendar widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Calendar extends WP_Widget {
	/**
	 * Ensure that the ID attribute only appears in the markup once
	 *
	 * @since 4.4.0
	 * @var int
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-recent-posts.php" line="2">

---

## WP_Widget_Recent_Posts

The `WP_Widget_Recent_Posts` class is used to implement a Recent Posts widget. It displays a list of your site's most recent posts.

```hack
/**
 * Widget API: WP_Widget_Recent_Posts class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Recent Posts widget.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Recent_Posts extends WP_Widget {

	/**
	 * Sets up a new Recent Posts widget instance.
	 *
	 * @since 2.8.0
```

---

</SwmSnippet>

<SwmSnippet path="/wp-includes/widgets/class-wp-widget-meta.php" line="2">

---

## WP_Widget_Meta

The `WP_Widget_Meta` class is used to implement a Meta widget. It displays log in/out, RSS feed links, etc.

```hack
/**
 * Widget API: WP_Widget_Meta class
 *
 * @package WordPress
 * @subpackage Widgets
 * @since 4.4.0
 */

/**
 * Core class used to implement a Meta widget.
 *
 * Displays log in/out, RSS feed links, etc.
 *
 * @since 2.8.0
 *
 * @see WP_Widget
 */
class WP_Widget_Meta extends WP_Widget {

	/**
	 * Sets up a new Meta widget instance.
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBbXl3ZWJzaXRlZGVtbyUzQSUzQWdpbGFkbmF2b3Q=" repo-name="mywebsitedemo" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
