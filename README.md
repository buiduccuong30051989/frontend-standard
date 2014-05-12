KA+A Front-End Development Standards
=================

Internal Note: Compiling rules and ideas in the readme for now, to make sure we're all on the same page.

Documented here are the standards for front-end development both defined and used by [KA+A](http://kaplusa.com). Before reading this, you should be familiar with Responsive Web Design, media queries, and SASS (specifically the [SCSS](http://sass-lang.com/) syntax).

## General Rules

### Indentation

Unless the environment requires otherwise (ruby, for example), use 4 space soft tabs for indentation of all code.

### Double Quotes vs. Single Quotes

Use double quotes (") rather than single quotes (') for anything that needs to be wrapped in quotes (HTML attributes, for example).

### Hyphens vs. Underscores

For naming files, classes or IDs, use hyphens (-) rather than underscores (_). The only time you should use an underscore in naming is to prefix a partial (for example: _header.html or _header.php)

## CSS Rules

### SASS (SCSS)

Use the SCSS syntax of SASS and separate your stylesheets by the sections or modules they are targeting. A few stylesheets should always be present:

* mixins.scss - declare the primary color palette and font stack variables, as well as mixins for media queries and any other styles that are used across multiple types of elements.
* global.scss - for styling elements without classes (H1 through H4, .container, etc...)
* print.scss - for print styles

### Nesting and Spacing and Multiple Selectors

Nest your SASS. 

Do this:

	body {
		header {
		}
	}

Not this:

	body header {
	}

For spacing, this:

	ul,
	ol {
	}

Not this:

	ul, ol {
	}
	
Also, add a line break before starting a new declaration with properties. In other words, this:

	ul {
		property:;
		
		li {
			property:;
		}
	}
	
Not this:

	ul {
		property:;
		li {
			property:;
		}
	}
	
This is fine:

    ul {
        li {
            property:;
        }
    }
    
### Media Queries

Declare media queries as mixins in mixins.scss. Go mobile first. (for example: base styles, 400up, 600up, 1000up...)

Media queries should be nested and organized with the elements they are affecting. Read [Chris Coiyer's article](http://css-tricks.com/conditional-media-query-mixins/) for details.

### Sizing Units

Use percentages for widths, unless a special case dictates otherwise.

Use EMs for font-size, line-height, height, and any height-based style. Keep the base font size at 16px so we can use the Bourbon mixin, em().

### Property Order

Group CSS properties in the following order:

	selector {
		
		// Content
		content:;
		
		// Positioning
		position:;
		top:;
		right:;
		bottom:;
		left:;
		display:;
		float:;
		clear:;
		
		// Sizing
		width:;
		height:;
		overflow:;
		padding:;
		margin:;
		
		// Font
		font:;
		line-height:;
		color:;
		text-shadow:;
		
		// Background and borders
		background:;
		border:;
		border-radius:;
		box-shadow:;
		
		// Transitions
		transitions:;

	}

(Note: Comments are for purposes of the style guide only. No need to comment each group of properties in your actual code.)

## HTML Rules

### Classes vs IDs

Classes are for styling elements. IDs are for targeting elements with javascript.

### Aria Roles

Include aria roles for accessibility. [See here](http://rawgit.com/w3c/aria-in-html/master/index.html) for more information on when/where/how to use.

### Optional Closing Tags

Even though omitting some closing tags is syntactically correct, include them anyways for clarity.

Do this:

	<li>List Item</li>

Not this:

	<li>List Item
	
On the other hand, do not close self-closing elements, such as the image or horizontal rule tags.

Do this:

    <hr>

Not this:

    <hr />

### Responsive Images

#### Vector

Use inline SVG for vector images. Provide a fallback for IE8. To keep code maintainable, use PHP or Hammer includes rather than pasting the entire inline SVG in the HTML.

#### Raster

Use the picture element to provide the optimal image sizes and crops for different breakpoints and resolutions. For a fallback, use picturefill.js

### Attribute Order

For consistency, HTML attributes should be written in the following order:

* class
* id, name
* data-*
* src, for, type, href
* title, alt
* aria-*, role

For example:

    <nav class="main-nav" role="navigation"
        <a class="btn" id="menu-toggle" data-toggle="dropdown" href="#" role="button">
        <input id="first-name" name="first-name" type="text" />
    </nav>
