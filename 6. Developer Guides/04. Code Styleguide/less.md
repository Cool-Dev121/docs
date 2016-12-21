# Rocket.Chat Less Styleguide

- [Comments](#comments)
- [Formatting](#formatting)
- [Selectors](#selectors)
- [Properties](#properties)
- [Colors](#colors)

## Comments

* Prefer line comments (`//`) to block comments.
* Prefer comments on their own line. Avoid end-of-line comments.
* Write detailed comments for code that isn't self-documenting:
  - Uses of z-index
  - Compatibility or browser-specific hacks

## Formatting

* Use tabs for indentation
* Use dashes over camelCasing in class names.
* Prefer to not use ID selectors
* When using multiple selectors in a rule declaration, give each selector its own line.
* Put a space before the opening brace `{` in rule declarations
* In properties, put a space after, but not before, the `:` character.
* Put closing braces `}` of rule declarations on a new line
* Put blank lines between rule declarations, but not in nesting selectors.
* Put nesting after all properties.
* Try to not use `!important`.
* Lowercase, always :)

**Bad**

```less
blockquote {
	.clearfix;
	margin: .5em 0;
	&:first-child {
		margin-top: 0;
	}
	&:last-child {
		margin-bottom: 0;
	}
	padding-left: 10px;
	position: relative;
	&:before {
		content: ' ';
		width: 4px;
		position: absolute;
		border-radius: 2px;
		left: 0;
		top: -1px;
		bottom: -1px;
	}
}
.login-terms {
	font-size: smaller;
	width: 520px;
	padding: 10px;
	max-width: 100%;
	margin: auto;
	a {
		font-weight: bold !important;
		text-decoration: underline;
	}
}
```

**Good**

```less
blockquote {
	.clearfix;
	margin: .5em 0;
	padding-left: 10px;
	position: relative;

	&:first-child {
		margin-top: 0;
	}

	&:last-child {
		margin-bottom: 0;
	}

	&::before {
		content: ' ';
		width: 4px;
		position: absolute;
		border-radius: 2px;
		left: 0;
		top: -1px;
		bottom: -1px;
	}
}

.login-terms {
	font-size: smaller;
	width: 520px;
	padding: 10px;
	max-width: 100%;
	margin: auto;

	a {
		font-weight: bold;
		text-decoration: underline;
	}
}
```

## Selectors

### Create an empty line before selectors.
**Bad**

```less
.class {
	border: 0;
}
.second-class: {
	text-align: right;
}
```

**Good**

```less
.class {
	border: 0;
}

.second-class: {
	text-align: right;
}
```

### Use a single space after selectors.
**Bad**

```less
.class{
	border: 0;
}
```

**Good**

```less
.class {
	border: 0;
}
```

### Add an empty line before nested selectors.
**Bad**

```less
.class {
	border: 0;
	&.another-class {
		color: #ffffff;
	}
}
```

**Good**

```less
.class {
	border: 0;

	&.another-class {
		color: #ffffff;
	}
}
```

### Use an empty line before non-nested selectors.
**Bad**

```less
.class {
	border: 0;

	&.another-class {
		color: #ffffff;
	}
}
.logo {
	display: block;
}
```

**Good**

```less
.class {
	border: 0;

	&.another-class {
		color: #ffffff;
	}
}

.logo {
	display: block;
}
```

### Don’t add whitespaces inside of the brackets within attribute selectors.
**Bad**

```less
.input[ type="text" ] {
	border: 0;
}
```

**Good**

```less
.input[type="text"] {
	border: 0;
}
```

### Don’t add a whitespace between operators within attribute selectors.
**Bad**

```less
.input[type = "text" ] {
	border: 0;
}
```

**Good**

```less
.input[type="text"] {
	border: 0;
}
```

### Always use a single space between the combinators of selectors.
**Bad**

```less
.class>.button {
	font-size: 1rem;
}
```

**Good**

```less
.class > .button {
	font-size: 1rem;
}
```

### Add a newline after the commas of selector lists.
**Bad**

```less
.class,  .another, .another-class {
	padding: 1.5rem;
}
```

**Good**

```less
.class,
.another,
.another-class {
	padding: 1.5rem;
}
```

### Don’t add a whitespace inside of the parentheses within pseudo-class selectors.
**Bad**

```less
.class:not( .another ) {
	margin: 5px;
}
```

**Good**

```less
.class:not(.another) {
	margin: 5px;
}
```

### Double colon for applicable pseudo-elements.
**Bad**

```less
.class:before {
	border-width: 2px;
}

.class:first-child {
	color: #000000;
}
```

**Good**

```less
.class::before {
	border-width: 2px;
}

.class:first-child {
	color: #000000;
}
```

## Properties

### Don’t add empty line in first/last property or in between properties.
**Bad**

```less
.room-list {

	border: 0;
	padding-left: 0;

	color: #ddfc32;

}
```

**Good**

```less
.room-list {
	border: 0;
	padding-left: 0;
	color: #ddfc32;
}
```

### Don't add properties in single-line. Use one property per line.
**Bad**

```less
.sumbit {color: #ffffff; background-color: #000000;}
```

**Good**

```less
.sumbit {
	color: #ffffff;
	background-color: #000000;
}
```

### No empty blocks.
**Bad**

```less
.button {}
```

**Good**

```less
.button {
	float: left;
}
```

### Longhand properties must be combined into one shorthand property.
**Bad**

```less
.class {
	padding-left: 12px;
	padding-top: 5px;
	padding-bottom: 8px;
}
```

**Good**

```less
.class {
	padding: 5px auto 8px 12px;
}
```

### Don’t use shorthand properties that override related longhand properties.
**Example**

```less
.class {
	border-color: #ffffff;
	border: 1px solid #000000;
}
```

### Always add a trailing semicolon in the end of a declaration.
**Bad**

```less
.another-class {
	color: #ffffff;
	padding: 2px
}
```

**Good**

```less
.another-class {
	color: #ffffff;
	padding: 2px;
}
```

### Add a newline after the colon of declarations.
**Bad**

```less
.another-class {
	box-shadow: 0 0 0 1px #5b9dd9, 0 0 2px 1px rgba(30, 140, 190, 0.8);
}
```

**Good**

```less
.another-class {
	box-shadow:
		0 0 0 1px #5b9dd9,
		0 0 2px 1px rgba(30, 140, 190, 0.8);
}
```

### Don’t duplicate properties within declaration blocks.
**Bad**

```less
.another-class {
	display: block;
	margin-top: 2rem;
	display: inline-block;
}
```

**Good**

```less
.another-class {
	margin-top: 2rem;
	display: inline-block;
}
```

### Don’t duplicate selectors along the file.
**Bad**

```less
.some-class {
	display: block;
}
.another-class {
	position: absolute;
}
.some-class {
	margin-top: 2rem;
	display: inline-block;
}
```

**Good**

```less
.some-class {
	display: block;
	margin-top: 2rem;
	display: inline-block;
}
```

### Add a whitespace before bang (!) declaration.
**Bad**

```less
.class {
	margin-left: 12px!important;
}
```

**Good**

```less
.class {
	margin-left: 12px !important;
}
```

### Use spaces around calc operators.
**Bad**

```less
.class {
	width: calc(~"200px-1rem");
}
```

**Good**

```less
.class {
	width: calc(~"200px - 1rem");
}
```

### Remove units for zero lengths.
**Bad**

```less
.button {
	padding: 10px 0px 0px 2px;
}
```

**Good**

```less
.button {
	padding: 10px 0 0 2px;
}
```

### Use a leading zero for fractional numbers less than 1.
**Bad**

```less
.message-form {
	margin-right: .5rem;
}
```

**Good**

```less
.message-form {
	margin-right: 0.5rem;
}
```

### Don’t add trailing zeros in numbers.
**Bad**

```less
.flex-tab {
	padding-bottom: 1.500rem;
}
```

**Good**

```less
.flex-tab {
	padding-bottom: 1.5rem;
}
```

### Don’t add newlines in strings.
**Bad**

```less
.nav-link::before {
	content: "sample
		text";
}
```

**Good**

```less
.nav-link::before {
	content: "sample text";
}
```

## Colors
### Lowercase, always.
### Long notation.
**Bad**

```less
.another-class {
	background-color: #FFF;
}
```

**Good**

```less
.another-class {
	background-color: #ffffff;
}
```
