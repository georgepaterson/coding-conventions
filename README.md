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
	
The HTML5 specification eliminates the Document Type Declaration. Although HTML5 is case insensitive we retain the formal syntax to allow the document to be parsed as XML.

### Page title

Every page should contain a title tag in the head of the document.

	<title>Briefly describing the content of the page</title>
	
The title tag should uniquely but briefly describe the content of the page.

### Charset meta tag

The charset meta tag is required to define the character set used by the document.

	<meta charset="utf-8">

### Description meta tag

Every page should contain a description meta tag in the head of the document.

	<meta name="description" content="Uniquely and accurately summarise the page content.">
	
The description meta tag should uniquely and accurately summarise the page content. At a minimum it should be a sentence, at most a short paragraph.

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
			<meta charset="utf-8">
			<meta name="description" content="Complexity of the DOM should be reduced.">
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
			<meta charset="utf-8">
			<meta name="description" content="DOM has been reduced to the elements required to describe the page.">
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
	
By putting all the CSS properties on a single line this makes it impossible for revision control to identify changes to individual properties. Single line CSS will also fail line length conventions for complex styling. If you need to scan selectors, leverage your code editor, for instance Textmate's 'Go To Symbol' navigation option will let you traverse the file by selector. 
	
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

Indenting CSS to the refer to the structure of the DOM tree only implies a relationship and but does not enforce that relationship; while a complex DOM tree will lead to a complex tab order that may be difficult to understand. 

It is preferred that multiple line formatting is used without indentation.

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
	
Hyphen separated:	
	
	.product-list {
		display: block; 
		margin: 0 10px;
		width: 510px;
	}
	
Hyphen separated is the preferred method, using the naming style of the HTML and CSS languages.

### Specificity

Specificity is used in CSS to calculate which selector should apply to a given element, with the higher specificity winning. 

The specific values for each type. [[2](#note-2)] 

* ID selectors in the selector = 100
* Class selectors, attributes selectors, and pseudo-classes in the selector = 10
* Type selectors and pseudo-elements in the selector = 1

Example specificity.

	/* 1 HTML selector, a specificity of 1 */
	section
	/* 1 class selector, a specificity of 10 */
	.facet
	/* 1 ID selector, a specificity of 100 */
	#facet-navigation
	/* 2 HTML selectors, a specificity of 2 */
	nav section
	/* 1 ID selector, 1 class selector, a specificity of 110 */
	#facet-navigation .facet
	/* 2 HTML selectors, 1 ID selector, 1 class selector, a specificity of 112 */
	nav#facet-navigation section.facet

Selectors with equal specificity will respect the cascade. Selectors with greater specificity will not respect selectors with lesser specificity in the cascade.

It is not recommended selectors are over specified as this will make the style sheet difficult to maintain.
	
### !important

The !important rule when applied to a CSS property will override the property value applied through specificity and the cascade. Overriding specificity and the cascade significantly increases the effort in maintaining the code.

The !important rule must be avoided.

### Units of measurement

When choosing a unit of measurement by consistent in using that unit throughout a project, unless absolutely necessary. Mixed units increase the conceptual complexity of a property.

Em units applied to an element, inherit their value from their parent element, with a complex DOM this can make em units inaccurate and difficult to use. This also applies to percentage units.

Root em units avoid this as the value is relative to the root element and not any parent elements. Root em units do not have sufficient cross browser support for production use. 

Pixels units do not have inheritance issues and are the preferred unit of measurement. Line-height is the exception to this and should be unit-less.  

### CSS comments

CSS comments can either be single line or multiple line. All comments should be made before the code they are describing.

Single line comments should describe single selectors, avoid describing properties.

	/* Single line comment. */

Multiple line comments should describe complex CSS blocks.

	/*
		Multiple line comment.
		Should be used to describe complex CSS blocks.
	*/

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

### CSS resets

CSS resets are a great source of information on default browser styles but in attempting to set a baseline for every possible element, this can increase the complexity of the style sheet, decrease performance and elements not styled lose browser fallback styling. If general styles are required they should be apparent through commonalities found in your selectors and properties within the style sheets. 

Third party CSS resets should be avoided. 

### CSS validation

The progressive implementation of the CSS specification, browser specific features and vendor prefixing makes automated conformance to a specification difficult. CSS quality analysis is preferred.   

### CSS quality analysis

CSS quality analysis is preferred over simple validation. 

Manual review of CSS architect should be undertaken on a regular basis, CSSLint should form part of the Continuous Integration strategy. 

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
	
Variables can be declared simply by naming the identifier, creating a global variable. However global variables should be avoided, locally scoped variables using var are preferred.

	example = 'value';

#### Constants

The constant declaration will be available in ECMAScript 6 and currently has partial cross browser support.

	const EXAMPLE_CONSTANT = 'value';

The convention for naming constant identifiers is in CAPS with an underscore used to join words. Do not use uppercase to name variables.	

#### Arrays

The predefined Array object is a constructor with it's own properties and methods. An array can be created with the Array constructor.

	var example = new Array();
	
However it is preferred to create an array using the literal notation. 
	
	var literal = [];
	
An array literal can be created with specified values. 
	
	var literal = [one, two, three];

#### Objects

The predefined Object is a constructor with it's own properties and methods. An object can be created with the Object constructor.

	var example = new Object();
	
However as with arrays it is preferred to create an object using the literal notation.	
	
	var literal = {};
	
An object literal can be created with a name/value pairing. The name can be an identifier or string, the value can be a property or a function.
	
	/* Name one identifier with string value. */
	var literal = {one: 'test'};
	/* Name 'two' string with a string value. */
	var literal = {'two': 'test'};
	/* Name three identifier with a named function as the value. */
	function test() {};
	var literal = {three: test()};
	/* Name four identifier with a anonymous function as the value. */
	var literal = {four: function () {}};
	/* All examples combined. */
	function test() {};
	var literal = {one: 'test', 'two': 'test', three: test(), four: function () {}};

### Functions

Functions can be written either as function declarations.

	function example(options) {
		statement;
	}

Or as function expressions.

	var example = function (options) {
		statement;
	}
	
Although function expressions can be given a name. 

	var example = function demo(options) {
		statement;
	}

Anonymous function expressions are preferred as the function is referenced by a single identifier.	

### Constructors

A constructor is a function designed to initialise an object with predefined properties using the new operator. Constructor functions use Pascalase where the first character is capitalised.

The example identifier uses the predefined Object constructor.

	var example = new Object();

An Audio function is designed as a constructor. The audio identifier is then initialised with the Audio constructor, this sets the volume property on audio. 
	
	function Audio() {
		this.volume = function() {};
	}
	var audio = new Audio();
	audio.volume();	
	
### Statements

The following statements should take the form described below.

#### If statement

If statement.

	if (condition) {
		statement;
	}

If statement with else.

	if (condition) {
		statement;
	} else {
		statement;
	}
	
If statement with additional condition and else.

	if (condition) {
		statement;
	} else if (condition) {
		statement;
	} else {
		statement;
	}
	
#### Switch statement

	switch (expression) {
		case label:
			statement;
			break;
		case label:
			statement;
			break;
		default:
			statement;
	}
	
Each group of statements should end with break, return or throw.

#### For statement

	for (expression; condition; expression) {
		statement;
	}

#### While statement

	while (condition) {
		statement;
	}

#### Do statement

	do {
		statement;
	} while (condition);
	
#### Try statement

Exception handling with a try statement.

	try {
		statement;
	} catch (exception) {
		statement;
	}
	
Try statement with finally block.	
	
	try {
		statement;
	} catch (exception) {
		statement;
	} finally {
		statement;
	}

### Conditional operator

The conditional operator is a ternary operator and can be used as a short form if...else statement.

	condition ? expression1 : expression2
	
It is recommended that if...else statements rather than the conditional operator are used as it improves the readability of the code.  

### Eval

Eval is a predefined JavaScript function.

	eval(string);
	
Eval will evaluate a string passed to it as if it was JavaScript code. It is an incredibly powerful function; however because it will evaluate any string as JavaScript it is a risk vector for poorly written or malicious code.

Eval should be avoided.

### Reserved words

Reserved words are restricted for use as identifiers, ECMAScript specifies current of future use for them [[3](#note-3)]. Identifiers are used for variables, constants, function declarations, function expressions, conditional statements and loops statements.

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
* class
* enum
* [export](https://developer.mozilla.org/en/JavaScript/Reference/Statements/export)
* extends
* [import](https://developer.mozilla.org/en/JavaScript/Reference/Statements/import)
* super
* implements
* interface
* [let](https://developer.mozilla.org/en/JavaScript/Reference/Statements/let)
* package
* private
* protected
* public
* static
* [yield](https://developer.mozilla.org/en/JavaScript/Reference/Statements/yield)
* undefined

### JavaScript comments

JavaScript comments can either be single line or multiple line. All comments should be made before the code they are describing.

Single line comments should describe simple functions, statements or variables.

	// Single line comment.

Multiple line comments should describe complex behaviour.

	/*
		Multiple line comment.
		Should be used to describe complex behaviour.
	*/

### JavaScript quality analysis

The architecture of JavaScript modules should be modular [[4](#note-4)], leveraging object oriented design patterns [[5](#note-5)].

All JavaScript committed to the project repository must be linted for code quality, [JSLint](http://www.jslint.com/) is the preferred linting tool. Linting should be performed as part of the Continuous Integration process.

JavaScript modules should have associated unit test, this will allow easy identification of module failure.

## Notes

1. Specific revision control system option is dependent on project requirements.
2. [Calculating a selector's specificity](http://www.w3.org/TR/2009/PR-css3-selectors-20091215/#specificity)
3. [Reserved Words - MDN](https://developer.mozilla.org/en/JavaScript/Reference/Reserved_Words)
4. [Object Oriented JavaScript: Modular development](http://www.georgepaterson.com/2011/07/17/object-oriented-javascript-modular-development/)
5. [Design Patterns](http://en.wikipedia.org/wiki/Design_Patterns_%28book%29)

## Developer resources

1. [Mozilla Developer Network](https://developer.mozilla.org/)
2. [Code Conventions for the JavaScript Programming Language](http://javascript.crockford.com/code.html)
3. [JavaScript The Definitive Guide](http://www.amazon.co.uk/JavaScript-Definitive-Guide-David-Flanagan/dp/0596101996)
