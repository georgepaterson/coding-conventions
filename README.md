# Coding conventions

## Purpose of this document

This document outlines [coding conventions](http://en.wikipedia.org/wiki/Coding_conventions) and standards that are recommended for client side development. Coding to a convention is not a barrier to innovation, it is a living document that should be updated by new concepts and implementation patterns. Through maintaining conventions in development we support better understandability and maintainability of our code.

## General

### Revision control

Revision control should be used on all projects.   

Subversion and Git are recommended revision control systems. [[1](#note-1)] 

### Continuous integration

Continuous integration should be implemented for all projects. Code committed to revision control should be validated against international standards and best practice. If the code passes validation then it should be processed for deployment. Deployment process should include concatenation and minification.

### Coding style

Extension and maintenance of code is reliant on the developer understanding peer written code. Code should be self descriptive, use whitespace and include verbose commenting. Concatenation and minification of code before deployment will eliminate overhead on production code.   

### Indentation

Space characters should be used to indent code, tab characters should be avoided. Soft tabs are available in most development environments, soft tabs act like hard tabs but resolves to spaces. Default indentation is 4 spaces.

### Line length

Dynamic word wrapping and high resolution displays makes fixed line length for content obsolete. However in programming arbitrary wrapping can make code difficult to understand. Manual line breaks are preferred for code. 

In typography, the measure is a reference to the width of a column of text. The measure has an ideal range of 45 to 75 characters per line for optimal legibility. 

A default line length of 80 characters is recommend.

### File paths

All file paths should be absolute. Apache folder aliasing or IIS virtual folders can be used to map file paths, allowing files to be easily repositioned within the project folder structure.

Apache alias example:

	<VirtualHost *:80>
	    ServerName your-site.tld
	    DocumentRoot "/var/www/your-site"
		Alias /asset /path/to/asset
	</VirtualHost>
	
File reference for a project style sheet: 

	<link rel="stylesheet" href="/assets/theme/style/common.css?ver=1" media="screen">

Relative file paths are to be avoided.

### Hungarian notation

Hungarian notation is split in to the original Applications Hungarian outlined by Charles Simonyi and it's evolution to Systems Hungarian. Applications Hungarian prefixes the identifier with the logical data type so that the identifier's purpose can be understood. Systems Hungarian prefixes the identifier with the physical data type.

Examples of Applications Hungarian in JavaScript:

	/* Identifies the variable as representing a height */
	var hValue = value.getHeight();
	/* Identifies the variable as a difference between values */
	var dValue = firstValue - secondValue;
	
Applications Hungarian can be useful to the programmer in identifying the purpose of the variable, however when shortened to a prefix it loses semantic value as an initial lexicon may be required to decipher the prefix.

Examples of Systems Hungarian in JavaScript:

	/* An object */
	var oExample = {};
	/* An array */
	var aExample = [];
	/* A private variable */
	var _example = 'test';
	/* A jQuery object */
	var $example = $('#example');

In Systems Hungarian prefixing an identifier with the physical does not enforce type or privacy, this limits the value of the prefix. 

Identifiers should be named by what the do rather than what they are, where Applications Hungarian may have had value in a large scale development eco-system, Systems Hungarian lost this value.

Hungarian notation both Applications and Systems should be avoided.    

## HTML

### Doctype

The doctype should be the first element declared on the page and the HTML5 doctype should be used. 

	<!DOCTYPE html>
	
The HTML5 eliminates the Document Type Declaration. Although HTML5 is case insensitive we retain the formal syntax to allow the document to be parsed as XML.

### Syntax

Even though HTML5 is case insensitive all HTML tags and associated attributes should be lower case to improve readability.

Attributes should be fully defined with double quotes:

	<video autoplay="true"></video>
	
All tags, including optional tags, must have a start and end tag.

	<ul>
		<li>A closing list element may be optional but well structured code removes ambiguity.</li>
	</ul>

Single tags must be self closing.

	<input type="text" />

Descriptive syntax improves the understandability of the HTML document for distributed developers

### Document object model

The Document Object Model (DOM) is the fundamental structure for understanding objects and there associated methods within HTML and XML documents; we can interact with DOM through the use of JavaScript.

When constructing a HTML document it is vital the developer understands the DOM, every object placed within the document should have meaning and purpose. We wish to avoid an over complicated DOM for performance but also future maintenance; the code itself should be self describing.

This code uses more objects than is needed to describe the form. 

	<!DOCTYPE html>
	<html lang="en-GB" dir="ltr">
		<head>
			<title>An unnecessary complex DOM</title>
		</head>
		<body>
			<div>
				<form>
					<ul>
						<li>
							<div>
								<label></label>
								<input />
							</div>
						</li>
						<li>
							<div>
								<label></label>
								<input />
							</div>
						</li>
					</ul>
				</form>
			</div>
		</body>
	</html>
	
We should aim to reduce the number of objects used to only those required to describe the document. 

	<!DOCTYPE html>
	<html lang="en-GB" dir="ltr">
		<head>
			<title>A simple DOM</title>
		</head>
		<body>
			<form>
				<fieldset>
					<legend></legend>
					<label></label>
					<input />
					<label></label>
					<input />
				</fieldset>
			</form>	
		</body>
	</html>

Only if we are unable to style the objects with CSS or manipulate them with JavaScript should we chose to place additional objects in the DOM. Each choice must be justifiable. 

### HTML comments

HTML comments can either be single line or multiple line. All comments should be made before the code they are describing and share the same tab indent.

Single line comments should describe simple HTML constructs.

	<!-- Single line comment. -->
	
Multiple line comments should describe complex HTML constructs.
	
	<!--  
		Multiple line comment.
		Should be used to describe complex structures.
	-->
	
Comments should describe the purpose of the HTML construct but should not be so verbose as to make the HTML document unreadable. Comments can be removed during the build process before deployment.

### HTML validation

All HTML should be validated against the [HTML5 specification](http://validator.w3.org/).

Any HTML asynchronously injected in to the document should also be validated.

Validation should form part of the build process and failure to validate should cause the build to fail.

## CSS

### CSS formatting

There are several ways to format CSS. Two primary methods focus either on the selectors or the properties.

Single line formatting focuses on the selector.

	.product-list .product {background: #DDD; display: inline-block; margin: 0 10px 5px; width: 510px;}
	
Multiple line formatting focuses on the properties.

	.product-list .product {
		background: #DDD;
		display: inline-block;   
		margin: 0 10px 5px;
		width: 150px;
	}
	
Both single line and multiple line formatting can be indented to refer to the tree structure of the DOM.

	.product-list {display: block; margin: 0 10px; width: 510px;}
		.product-list .product {background: #DDD; display: inline-block; margin: 0 10px 5px; width: 510px;}
	
	.product-list {
		display: block; 
		margin: 0 10px;
		width: 510px;
	}	
		.product-list .product {
			background: #DDD;
			display: inline-block;   
			margin: 0 10px 5px;
			width: 150px;
		}

By putting all the CSS properties on a single line this makes it impossible for revision control to identify changes to individual properties. Single line CSS will also fail line length conventions for complex styling. If you need to scan selectors, leverage the power of your code editor, for instance Textmate's 'Go To Symbol' navigation option will let you traverse the file by selector. 

Indenting CSS to the refer to the structure of the DOM is an artificial process with not currently supported within the language. The choice of selector should be sufficient to understand it's position within the DOM.

It is therefore recommended that multiple line formatting is used without indentation.

	.product-list {
		display: block; 
		margin: 0 10px;
		width: 510px;
	}	
	.product-list .product {
		background: #DDD;
		display: inline-block;   
		margin: 0 10px 5px;
		width: 150px;
	}
	
### CSS property order

A consistent CSS property order will aid in the compression of the style sheet.

The recommended method to achieve this is to order properties alphabetically.

### Selector naming

A consistent naming convention should be used within a project. Selector names should have semantic value and be named by their purpose, not how they affect the visual design.

Selectors that use more than one word should use a clearly defined joining method. Three main methods are:

Camel case:

	.productList {
		display: block; 
		margin: 0 10px;
		width: 510px;
	}
	
Underscore separated:

	.product_list {
		display: block; 
		margin: 0 10px;
		width: 510px;
	}
	
Dash separated:	
	
	.product-list {
		display: block; 
		margin: 0 10px;
		width: 510px;
	}
	
Dash separated is the preferred method, using the naming style of the HTML and CSS languages.

### Specificity

### Units of measurement

### Box model

#### Block elements

#### Inline elements

#### Inline-block elements 

### CSS comments

CSS comments can either be single line or multiple line. All comments should be made before the code they are describing.

Single line comments should describe single selectors, avoid describing properties.

	/* Single line comment. */

Multiple line comments should describe complex CSS blocks.

	/*
		Multiple line comment.
		Should be used to describe complex CSS blocks.
	*/

### CSS resets

### CSS preprocessors

### !important

The !important rule when applied to a CSS property will override the property value applied through the cascade. Overriding the cascade significantly increases the effort in maintaining the code.

The !important rule must be avoided.

### Internet Explorer conditional comments

Conditional comments are a simple conditional statement that allows IE to read the content of a comment. It can be used to set IE specific hooks for CSS.

Although there are different methods for implementing conditional comments, the recommended approach is to set an IE specific classname on the HTML tag reducing the number of style sheet requests.

	<!--[if IE 7]><html class="ie7" lang="en-GB" dir="ltr"><![endif]-->
	<!--[if IE 8]><html class="ie8" lang="en-GB" dir="ltr"><![endif]-->
	<!--[if IE 9]><html class="ie9" lang="en-GB" dir="ltr"><![endif]-->
	<!--[if !IE]><!--><html lang="en-GB" dir="ltr"><!--<![endif]-->
	
Conditional comments will not be supported in [IE10](http://blogs.msdn.com/b/ie/archive/2011/07/06/html5-parsing-in-ie10.aspx).

### Internet Explorer compatibility mode

Internet Explorer can render as if it were a previous version without explicit instruction from the browser user. To prevent this, we inform the browser that the latest render engine version for the particular browser should be used. 

	<meta content="IE=edge" http-equiv="X-UA-Compatible">

### CSS validation

### CSS quality analysis

## JavaScript

### External files

All JavaScript should be referenced through external files. This improves maintenance of the project and files can be referenced after the DOM is loaded.

When referencing a JavaScript file the type and charset attribute is no longer necessary.

The obsolete attributes:

	<script src="example.js" type="text/javascript" charset="utf-8"></script>
	
The simplified reference:

	<script src="example.js"></script> 

### Variable declarations

Variables should be declared before use to prevent hoisting and declared as close as possible to where you will use them.

Variables should be declared with a lower case letter and the identifier should have semantic value.

	var example = 'value';
	
Use camel case to join words in a variable declaration.

	var exampleVariable = 'value';

#### Constants

The constant declaration will be available in ECMAScript 6 and currently has partial cross browser support.

	const EXAMPLE_CONSTANT = 'value';

The convention for naming constant identifiers is in CAPS with an underscore used to join words. Do not use uppercase to name variables.	

#### Arrays

#### Objects

### Functions

Functions can be written either as function declarations.

	function example (options) {
		statement;
	}

Or as function expressions.

	var example = function (options) {
		statement;
	}
	
Although function expressions can be given a name. 

	var example = function demo (options) {
		statement;
	}

Anonymous function expressions are preferred as the function is referenced by a single identifier.	

### Constructors
	
### Closures

### Statements

#### If

	if (condition) {
		statement;
	}



	if (condition) {
		statement;
	} else {
		statement;
	}

#### Else if

	if (condition) {
		statement;
	} else if (condition) {
		statement;
	} else {
		statement;
	}
	
#### Switch

	switch (expression) {
		case label:
			statement;
			break;
		case label:
			statement;
			break;
		default:
			statement;
			break;
	}

#### For

	for (expression; condition; expression) {
		statement;
	}

#### While

	while (condition) {
		statement;
	}

#### Do

	do {
		statement;
	} while (condition);
	
#### Try

	try {
		statement;
	}
	catch (exception) {
		statement;
	}

### Operators

### Eval

Eval is a predefined JavaScript function.

	eval(string);
	
Eval will evaluate a string passed to it as if it was JavaScript code. It is an incredibly powerful function; however because it will evaluate any string as JavaScript it is a risk vector for poorly written or malicious code.

Eval should be avoided.

### Reserved words

* [break](https://developer.mozilla.org/en/JavaScript/Reference/Statements/break)
* [case](https://developer.mozilla.org/en/JavaScript/Reference/Statements/switch)
* [catch](https://developer.mozilla.org/en/JavaScript/Reference/Statements/try...catch)
* [continue](https://developer.mozilla.org/en/JavaScript/Reference/Statements/continue)
* [debugger](https://developer.mozilla.org/en/JavaScript/Reference/Statements/debugger)
* [default](https://developer.mozilla.org/en/JavaScript/Reference/Statements/switch)
* [delete](https://developer.mozilla.org/en/JavaScript/Reference/Operators/Special/delete)
* [do](https://developer.mozilla.org/en/JavaScript/Reference/Statements/do...while)
* [else](https://developer.mozilla.org/en/JavaScript/Reference/Statements/if...else)
* [finally](https://developer.mozilla.org/en/JavaScript/Reference/Statements/try...catch)
* [for](https://developer.mozilla.org/en/JavaScript/Reference/Statements/for)
* [function](https://developer.mozilla.org/en/JavaScript/Reference/Statements/function)
* [if](https://developer.mozilla.org/en/JavaScript/Reference/Statements/if...else)
* [in](https://developer.mozilla.org/en/JavaScript/Reference/Statements/for...in)
* [instanceof](https://developer.mozilla.org/en/JavaScript/Reference/Operators/Special/instanceof)
* [new](https://developer.mozilla.org/en/JavaScript/Reference/Operators/Special/new)
* [return](https://developer.mozilla.org/en/JavaScript/Reference/Statements/return)
* [switch](https://developer.mozilla.org/en/JavaScript/Reference/Statements/switch)
* [this](https://developer.mozilla.org/en/JavaScript/Reference/Operators/Special/this)
* [throw](https://developer.mozilla.org/en/JavaScript/Reference/Statements/throw)
* [try](https://developer.mozilla.org/en/JavaScript/Reference/Statements/try...catch)
* [typeof](https://developer.mozilla.org/en/JavaScript/Reference/Operators/Special/typeof)
* [var](https://developer.mozilla.org/en/JavaScript/Reference/Statements/var)
* [void](https://developer.mozilla.org/en/JavaScript/Reference/Operators/Special/void)
* [while](https://developer.mozilla.org/en/JavaScript/Reference/Statements/while)
* [with](https://developer.mozilla.org/en/JavaScript/Reference/Statements/with)


### JavaScript comments

JavaScript comments can either be single line or multiple line. All comments should be made before the code they are describing.

Single line comments should describe simple functions, statements or variables.

	// Single line comment.

Multiple line comments should describe complex behaviour.

	/*
		Multiple line comment.
		Should be used to describe complex behaviour.
	*/

### JavaScript abstraction

#### JavaScript libraries

#### JavaScript preprocessors

### JavaScript quality analysis

## Notes

1. Specific revision control system option is dependent on project requirements.

## Developer resources

1. [Mozilla Developer Network](https://developer.mozilla.org/)
2. [Code Conventions for the JavaScript Programming Language](http://javascript.crockford.com/code.html)
