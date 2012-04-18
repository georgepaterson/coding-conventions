# Coding standards

## Purpose of this document

This document outlines coding standards and conventions that are recommended for client side development. Coding to a standard is not a barrier to innovation, it is a living document that should be updated by new concepts and implementation patterns. Through maintaining standards in development we support better understandability and maintainability of our code.

## General

### Revision control

Revision control should be used on all projects.   

Subversion and Git are recommended revision control systems. [[1](#note-1)] 

### Continuous integration

Continuous integration should be implemented for all projects. Code committed to revision control should be validated against international standards and best practice. If the code passes validation then it should be processed for deployment. Deployment process should include concatenation and minification.

### Coding style

Extension and maintenance of code is reliant on the developer understanding their peers code. Code should be self descriptive, use whitespace and include verbose commenting. Concatenation and minification of code before deployment will eliminate overhead on production code.   

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
	    <Directory "/var/www/html/your-site">
	        Options Indexes FollowSymLinks +Includes ExecCGI
	        AllowOverride All
	        Order allow,deny
	        Allow from all
	    </Directory>
	</VirtualHost>
	
File reference for a project style sheet: 

	<link rel="stylesheet" href="/assets/theme/style/common.css?ver=1" media="screen">

Relative file paths are to be avoided.  

## HTML

### Doctype

The doctype should be the first element declared on the page and the HTML5 doctype should be used. 

	<!DOCTYPE html>
	
The HTML5 eliminates the Document Type Declaration. Although HTML5 is case insensitive we retain the formal syntax to allow the document to be parsed as XML.

### Syntax

Even though HTML5 is case insensitive all HTML tags and associated attributes should be lower case to improve readability.

Attributes should be fully defined with double quotes:

	<video autoplay="true"></video>
	
All tags must have a start and end tag including optional tags.

	<ul>
		<li>A closing list element may be optional but well structured code removes ambiguity.</li>
	</ul>

Single tags must be self closing.

	<input type="text" />

Descriptive syntax improves the understandability of the HTML document for distributed developers

### HTML formatting

### Document object model

### HTML comments

### HTML validation

## CSS

### CSS formatting

#### Standard formatting

#### Single line formatting

#### Indented formatting

### Selectors

### Selector naming

### Specificity

### Units of measurement

### Box model

#### Block elements

#### Inline elements

#### Inline-block elements 

### CSS naming

### CSS comments

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

#### Revision numbers

### JavaScript libraries

### JavaScript naming

### Variable and function names

#### Hungarian notation

### Variable declarations

#### Arrays

#### Objects

### Function declarations

### Statements

#### If

##### Ternary operator

#### For

#### While

#### Do

#### Switch

#### Try

### Operators

### Eval

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

### JavaScript quality analysis

## Notes

1. Specific revision control system option is dependent on project requirements.

## References
