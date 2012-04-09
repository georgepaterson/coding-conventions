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

## HTML

### Doctype

### Syntax

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

### !important

The !important rule when applied to a CSS property will override the property value applied through the cascade. Overriding the cascade significantly increases the effort in maintaining the code.

The !important rule must be avoided.

### Internet Explorer conditional comments

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

### JavaScript comments

### JavaScript quality analysis

## Notes

1.	Specific revision control system option is dependent on project requirements.

## References
