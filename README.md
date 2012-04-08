# Coding standards

## Purpose of this document

This document outlines coding standards and conventions that are recommended for client side development. Coding to a standard is not a barrier to innovation, it is a living document that should be updated by new concepts and implementation patterns. Through maintaining standards in development we support better understandability and maintainability of our code.

## General

### Indentation

### Line length

### Compression and minification

### Naming

#### Hungarian notation  

## HTML

### Doctype

### Syntax

### Document object model

### HTML comments

### HTML validation

## CSS

### CSS formatting

#### Standard formatting

#### Indented formatting

#### Single line formatting

### Selectors

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

The !important rule when applied to a CSS property will override properties applied through the cascade. Overriding the cascade significantly increases the effort in maintaining the code.

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

## References