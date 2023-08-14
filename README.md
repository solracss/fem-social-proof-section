# Frontend Mentor - [4 card feature section.](https://github.com/solracss/fem-4-card-feature-section)

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)

## Overview

### The challenge

Build out the project to the designs provided.
Your users should be able to:

- View the optimal layout for the page depending on their device's screen size

### Screenshot

<details>

<summary>Click to open</summary>

![Desktop]()
![Mobile]()

</details>

### Links

- Live Site URL: [Live](https://solracss.github.io/fem-4-card-feature-section/)

## My process

### Built with

[![My Skills](https://skillicons.dev/icons?i=html,css,sass,vscode,vite)](https://skillicons.dev)

### Notes

First time used `vite` for compiling sass and running site.

### What I learned

1. Structure `.scss` files in more organised way, think more globally when applying styles.

2. Define container with `min` function with auto padding and inline margin:

```css
.container {
	$max-width: 1100px;
	$padding: 4rem;

	width: min(100% - $padding, $max-width);
	margin-inline: auto;
}
```

3. Use custom properties and scss loop for setting top border color for each card

```html
<div class="card" data-card-accent="1">
	...
	<div class="card" data-card-accent="2">
		...
		<div class="card" data-card-accent="3">
			...
			<div class="card" data-card-accent="4">..</div>
		</div>
	</div>
</div>
```

```css
.card {
  ...
	border-top: 3px solid var(--item-color);

	@for $i from 1 through 4 {
		&[data-card-accent="#{$i}"] {
			--item-color: var(--clr-accent-#{$i});
		}
	}
}
```

4. Refactor this loop to use only sass variables

```scss
$colors: (
	clr-accent-1: hsl(180, 62%, 55%),
	clr-accent-2: hsl(0, 78%, 62%),
	clr-accent-3: hsl(34, 97%, 64%),
	clr-accent-4: hsl(212, 86%, 64%),
);

.card {
	border-top: 3px solid;

	@for $i from 1 through length($colors) {
		$color-key: nth(map-keys($colors), $i);
		$color-value: map-get($colors, $color-key);

		&[data-card-accent="#{$i}"] {
			border-color: $color-value;
		}
	}
}
```

5. Start using BEM methodology

```scss
.card {
	...
	&__heading {
		...
	}

	&__description {
		...
	}

	&__icon {
		...
	}
}
```

6. Use `clamp()` for making heading font size responsive

```css
font-size: clamp(1.5rem, 1.1444rem + 1.5172vw, 2.1875rem);
```

Used [calculator](https://clamp.font-size.app) to make my life easier.

7. Use mixin for mediaquery along with predefined breakpoints as list

```css
$breakpoints: (
	large: 68.75em,
	xtra-large: 72.8125em,
);

@mixin media($size) {
	@if map.has-key($breakpoints, $size) {
		$breakpoint: map-get($breakpoints, $size);
		@media screen and (min-width: $breakpoint) {
			@content;
		}
	} @else {
		@error 'the keyword #{$size} is not in the $breakpoints map';
	}
}
```
