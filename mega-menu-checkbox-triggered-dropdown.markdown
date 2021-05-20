---
layout: page
title: Mega menu checkbox-triggered dropdown
permalink: /mega-menu-checkbox-triggered-dropdown/
---

This page gives details about the **mega menu checkbox-triggered dropdown** component.

Note: Before we even begin, please note that we're using the Eric Meyer's CSS reset file and that's the starting point of all the other work in the Nimble CSS component library.

## The goal

In the **main menu hover dropdown component**, we showcased how to build a sub-navigation dropdown from a top-level `li` item, triggered to appear on mouse hover. 

However, this is not really too good of a solution, because it doesn't work too good on mobile (since mobile has no mouse pointer) - and also because it doesn't work too good with the keyboard either (so a11y is a second issue with the **main menu hover dropdown** component).

## The HTML structure

What we're trying to achieve, written in Emmet-like pseudo-code:
* Have a navigation consisting of `nav > ul > li` structure
* Some of the `li` items in the above structure contain the following sub-structure: `li > ul > li + li + li`
* The above nesting pattern might repeat over and over again

Here's a sample pseudo-code structure:
```
body
	header
		nav
			ul
				li
				li
				li
					ul
						li
						li
						li
				li
```

## The styling

How do we want this styled? 

We might want to keep the structure and styling of the **mega menu hover dropdown**, but this would beat the purpose of this project.

Instead, we'll focus on offering an alternative approach of achieving the same result as the **mega menu hover dropdown** component, but this one will **only work with checkbox triggers on click**.

Ideally, in production, we should build a structure that combines the **mega menu hover dropdown** and **mega menu checkbox triggered dropdown**.


## The HTML code

Here's the simplified HTML code (stripped of any attributes, images, icons, or anchor tags). Note: it's exactly the same HTML code as in the **main menu hover dropdown** component.
```html
<body>
	<header class="page-header-wrap">
		<nav class="mega-menu-checkbox-triggered-dropdown">
			<ul>
				<li>
					<ul>
						<li></li>
						<li></li>
					</ul>
				</li>
				<li></li>
				<li>
					<ul>
						<li></li>
						<li></li>
					</ul>
				</li>
			</ul>
		</nav>
	</header>
</body>
```

The only CSS classes we used above are the `page-header` class and the `mega-menu-checkbox-triggered-dropdown` class.
* `page-header` describes the **component group**
* `mega-menu-checkbox-triggered-dropdown` describes the **specific component within the given component group**

There can be more fine-grained css classes, but this is enough for now.

## The logic of the checkbox hack

Here is as simple an explanation of the checkbox hack as possible.

To start off, let's examine the `input` HTML element:
```
<input>
```

This is a self-closing element, meaning, it doesn't have a closing tag.

The `input` element's purpose is to receive user input. User input can be of many varieties:
* a file
* a password
* plain text (default)

To determine if it's a password, a plain text input, or something else entirely, we use the `type` attribute.

The possible values of the `type` attribute are:
* button
* checkbox
* color
* date
* datetime-local
* email
* file
* hidden
* image
* month
* number
* password
* radio
* range
* reset
* search
* submit
* tel
* text
* time
* url
* week

A checkbox is a "variety" of the `input` HTML element. For example:
```
<input type="checkbox" id="our-checkbox">
```

We can also use the `label` element with the input, so that our code looks as follows:
```
<label for="our-checkbox">Our checkbox</label>
<input type="checkbox" id="our-checkbox">
```

Here's [a codepen](https://codepen.io/AjdinImsirovic/pen/jOBVVgG){:target="_blank"} with the above code.

If we click on the checkbox itself, it will toggle its state from checked to unchecked.

The exact same behavior is achieved if we click on **the text contained by the `label` element**.

Now, the trick with the checkbox hack is to [add another element](https://codepen.io/AjdinImsirovic/pen/wvJogWd){:target="_blank"}.

Our code now looks like this:
```html
<label for="our-checkbox">
  Our checkbox
</label>
<input type="checkbox" id="our-checkbox">
<div class="checkbox-controlled">
  We want to affect this element
  with our checkbox state
</div>
```

Now is the time to use CSS to react to a checkbox being checked or unchecked. Here's the code:
```
.checkbox-controlled {
  background: gray;
}
#our-checkbox:checked ~ .checkbox-controlled {
  background: orange;
}
```

Let's break down the code above. The `~` character (aka tilde) affects elements that share a parent element. In our case, the parent for the two elements is the `body` element.

The selector to the left of the `~` is above the selector to the right of the `~`. 

It doesn't have to be immediate (they can be separated by elements between them).

Now we can userstand this selector:
```
#our-checkbox:checked ~ .checkbox-controlled
```

This selector, translated to English, is like saying: *If you find an `input` with `type` of `checkbox`, and if that checkbox is checked, and if inside the same parent there is an element with class of `checkbox-controlled`, give it the following styling*.

In our case, the initial styling of `.checkbox-controlled` is `background: gray`, and due to higher specificity, the `#our-checkbox:checked ~ .checkbox-controlled` sets the custom styling to `background: orange` - but only when the "if checked" condition is satisfied.

Next, we need to hide the checkbox using CSS. But we still need to make it accessible to screen readers. So the best way to do it is to set its opacity to 0.

This brings us really close to the show/hide menu toggle using the checkbox hack. This time, instead of toggling the background color, we toggle the entire `ul` that's nested inside the parent `li` in the menu.

We'll start with the same HTML structure we had in the [mega menu on hover component](https://codepen.io/AjdinImsirovic/pen/oNZYwwg){:target="_blank"}.

After a number of tweaks, we'll end up with the [mega menu checkbox dropdown codepen](https://codepen.io/AjdinImsirovic/pen/mdWOMwx){:target="_blank"}.

Unfortunately, even though the checkbox hack works, it's not as good a solution as one might expect, due to not working as great when navigating with keyboards.

If only used with the mouse, it works without issues. However, sinc there are issues with the keyboard, that means we'll have to look at ways of improving the user experience.

### The tabindex attribute

Using [the tabindex attribute](https://www.unimelb.edu.au/accessibility/aria/wai-aria-keyboard-focus){:target="_blank"}, we can now make any element tabable, using `tabindex="0"`.

But [this improvement](https://codepen.io/AjdinImsirovic/pen/mdWOMwx){:target="_blank"} is as far as the checkbox hack takes us in our quest to make an accessible, CSS-only mega menu.

This means that we'll need to take our existing mega menu, and update it by first removing the checkbox hack code.

Let's start by replacing this code:
```
<label for="our-checkbox-1" tabindex="0">Quickstart
        <input type="checkbox" id="our-checkbox-1" class="our-checkbox" name="dropdown-one" style="position:absolute; left:0; opacity:0" />
				<ul class="checkbox-controlled">
```

...with this code:
```
<button
	type="button"
	class="dropdown__title"
	aria-expanded="false"
	aria-controls="quickstart-dropdown"
>
	Quickstart
</button>
```