# html_basics

# 1.  HTML Document Structure

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Title of the Document</title>
  </head>
  <body>
    <!-- Content goes here -->
  </body>
</html>

```

# 2.  Head Tags

```html
<meta> <!-- for meta information -->
<link> <!-- for linking CSS and other resources -->
<script> <!-- for JavaScript -->
```

# 3.  Text Tags

```html
<h1> - <h6> <!-- heading tags -->
<p> <!-- paragraph tag -->
<b> <!-- bold text -->
<i> <!-- italicized text -->
<u> <!-- underlined text -->
<s> <!-- strikethrough text -->
<sup> <!-- superscript text -->
<sub> <!-- subscript text -->
<blockquote> <!-- blockquote text -->
```

# 4.  Formatting Tags

```html
<a> <!-- anchor tag -->
<img> <!-- image tag -->
<br> <!-- line break tag -->
<hr> <!-- horizontal rule tag -->
```

# 5.  Lists

```html
<ul> <!-- unordered list -->
<ol> <!-- ordered list -->
<li> <!-- list item -->
```

# 6.  Tables

```html
<table> <!-- table element -->
<thead> <!-- table header -->
<tbody> <!-- table body -->
<tr> <!-- table row -->
<th> <!-- table header cell -->
<td> <!-- table data cell -->
```

# 7.  Forms

```html
<form> <!-- form element -->
<input> <!-- input field -->
<label> <!-- label for input field -->
<select> <!-- drop-down menu -->
<option> <!-- option for drop-down menu -->
<button> <!-- button element -->
<textarea> <!-- text area element -->
```

# 8.  Comments

```html
<!-- This is a comment -->
```

This is just a basic cheat sheet to get you started with HTML. There are many more tags and attributes available in HTML.


# 9.  Attributes

```html
class="classname" <!-- for CSS styling -->
id="elementid" <!-- for uniquely identifying an element -->
style="property:value;" <!-- for inline CSS styling -->
href="url" <!-- for links -->
src="url" <!-- for images and other media -->
alt="description" <!-- for alternative text for images -->
title="text" <!-- for tooltip text -->
target="_blank" <!-- for opening links in a new tab -->
```

# 10.  Semantic Tags

```html
<header> <!-- for header content -->
<nav> <!-- for navigation links -->
<main> <!-- for main content -->
<section> <!-- for grouping related content -->
<article> <!-- for a self-contained article or blog post -->
<aside> <!-- for related content that is not part of the main content -->
<footer> <!-- for footer content -->
```

# 11.  Audio and Video

```html
<audio> <!-- for audio files -->
<source> <!-- for specifying audio source and type -->
<video> <!-- for video files -->
<source> <!-- for specifying video source and type -->
```

# 12.  Inline Frames

```html
<iframe> <!-- for embedding another web page or document -->
```

# 13.  Metadata

```html
<meta charset="utf-8"> <!-- for specifying character encoding -->
<meta name="description" content="description"> <!-- for search engine optimization -->
<meta name="keywords" content="keywords"> <!-- for search engine optimization -->
```

# 14.  Deprecated Tags

```html
<center> <!-- for centering content (use CSS instead) -->
<font> <!-- for setting font properties (use CSS instead) -->
<s> <!-- for strikethrough text (use CSS instead) -->
```

# 15.  Accessibility Tags

```html
<nav role="navigation"> <!-- for navigation links -->
<main role="main"> <!-- for main content -->
<section role="region"> <!-- for grouping related content -->
<article role="article"> <!-- for a self-contained article or blog post -->
<aside role="complementary"> <!-- for related content that is not part of the main content -->
<footer role="contentinfo"> <!-- for footer content -->
```


# 16.  Input Types

```html
<input type="text"> <!-- for text input -->
<input type="email"> <!-- for email input -->
<input type="password"> <!-- for password input -->
<input type="number"> <!-- for number input -->
<input type="checkbox"> <!-- for checkbox input -->
<input type="radio"> <!-- for radio button input -->
<input type="submit"> <!-- for submit button -->
<input type="reset"> <!-- for reset button -->
<input type="file"> <!-- for file upload -->
<input type="date"> <!-- for date input -->
<input type="time"> <!-- for time input -->
<input type="datetime-local"> <!-- for date and time input -->
<input type="color"> <!-- for color input -->
<input type="range"> <!-- for range input -->
<input type="search"> <!-- for search input -->
<input type="tel"> <!-- for telephone input -->
```

# 17.  SVG

```html
<svg> <!-- for scalable vector graphics -->
<path> <!-- for creating shapes and lines -->
<rect> <!-- for creating rectangles -->
<circle> <!-- for creating circles -->
<ellipse> <!-- for creating ellipses -->
<polygon> <!-- for creating polygons -->
<polyline> <!-- for creating polylines -->
<line> <!-- for creating lines -->
```

# 18.  Canvas

```html
<canvas> <!-- for creating graphics and animations -->
```

# 19.  Deprecated Attributes

```html
bgcolor="color" <!-- for background color (use CSS instead) -->
border="value" <!-- for border (use CSS instead) -->
align="value" <!-- for alignment (use CSS instead) -->
```

# 20.  Math and Science

```html
<math> <!-- for displaying mathematical formulas -->
<mrow> <!-- for grouping mathematical expressions -->
<mfrac> <!-- for displaying fractions -->
<msup> <!-- for displaying superscripts -->
<sub> <!-- for displaying subscripts -->
<sup> <!-- for displaying superscripts -->
<chem> <!-- for displaying chemical formulas -->
<mi> <!-- for displaying mathematical variables -->
<mn> <!-- for displaying mathematical numbers -->
<mtext> <!-- for displaying non-mathematical text -->
```

# 21. \<div>

The `<div>` tag is one of the most commonly used HTML tags, and it is used to define a section or division of a web page. It does not have any specific meaning or semantic value, but it is often used to group related elements together for styling or scripting purposes. Here's an example:

```html
<div>
  <h1>My Heading</h1>
  <p>Some text...</p>
</div>
```

In the example above, the `<div>` tag is used to group the `<h1>` and `<p>` elements together. This can be useful if you want to apply the same styles or behavior to both elements, or if you want to manipulate the contents of the `<div>` element using JavaScript.