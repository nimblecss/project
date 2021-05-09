---
layout: page
title: Main menu hover dropdown
permalink: /main-menu-hover-dropdown/
---

This page gives details about the **main menu hover dropdown** component.

## The goal

We want a main navigation that would look like a single horizontal group of top-level ("first-level") links. 

Some of these first-level links can hold nested ("second-level") groups of links.

Potentially, we could add third, fourth, etc. level of nested groups of links.

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

We want it styled in such a way that the sub-level `ul` elements appear and reveal their content when we hover on the respective parent `li` elements.

For that to happen, we initially need to have the nested `ul` elements and all their content set to `display:none`.

Wehn we hover the respective wrapping `li` we need to toggle the wrapped `ul` from `display:none` to `display:block`.

## The HTML code

Here's the simplified HTML code (stripped of any attributes, images, icons, or anchor tags):
```html
<body>
	<header class="page-header-wrap">
		<nav class="main-menu-hover-dropdown">
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

The only CSS classes we used above are the `page-header` class and the `main-menu-hover-dropdown` class.
* `page-header` describes the **component group**
* `main-menu-hover-dropdown` describes the **specific component within the given component group**

There can be more fine-grained css classes, but this is enough for now.

Here's the SCSS code for the given HTML structure, implemented using the Nimble CSS philosophy:
```scss
// positioning //////////////////////////

// display & box model //////////////////

header {

	&.page-header-wrap {

		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}

	nav {

	    &.main-menu-hover-dropdown {
	
			ul {
	
			    display: flex;
    			flex-wrap: wrap;
    			padding-left: 0;

				li {

					padding-right: 1rem;

					&:last-child {

						padding-right: 0;
					}
				}
			}
		}
	}
}


// colors //////////////////////////////

header {
	&.page-header-wrap {
		background: lightgray;
	}
}

// typography ///////////////////////// 

header {
	&.page-header-wrap {
		font-family: Arial, sans-serif;
	}
}

// other //////////////////////////////

header {	
	&.page-header-wrap {}

	nav {

	    &.main-menu-hover-dropdown {
	
			ul {
				list-style: none;
    		}
    	}
    }
}
```

As a demo of this component, check out none other than this very website's main menu:
```
<header class="page-header-wrap">
	<nav class="main-menu-hover-dropdown">
		<ul>
			<li>
				<a href="/">Nimblecss.com</a>
			</li>
			<li>
				<a href="/quickstart">Quickstart</a>
				<ul>
					<li>
						<a href="#">
							Sample sub-link 1
						</a>
					</li>
					<li>
						<a href="#">
							Sample sub-link 2
						</a>
					</li>
				</ul>
			</li>
			<li>
				<a href="/philosophy">Philosophy</a>
			</li>
			<li>
				<a href="/components">Components</a>
			</li>
			<li>
				<a href="/examples">Examples</a>
			</li>
			<li>
				<a href="/showcase">Showcase</a>
			</li>
		</ul>
	</nav>
</header>
```

However, currently the sub-menu navigation is displayed as follows:
{:class="d-block"}
![Sub-menu navigation showing due to poor styling](/assets/img/main-menu-hover-dropdown/001.png)


However, we need to hide the sub-menu ul and show it only on hover.

That means we'll start off with sub-menu ul style set to `display: none`.

And once a user hovers on the given `ul` element's parent `li`, the `display: none` will change to `display: block`.

This means that our SCSS now looks as follows:
```scss
....
// display & box model //////////////////

header {

	&.page-header-wrap {

		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}

	nav {

	    &.main-menu-hover-dropdown {
	
			ul {
	
			    display: flex;
    			flex-wrap: wrap;
    			padding-left: 0;

				li {

					padding-right: 1rem;

					&:last-child {

						padding-right: 0;
					}

					ul {
						display: none;
					}

					&:hover {
						ul {
							display: block;
						}
					}
				}
			}
		}
	}
}

....
```

The four dots, `....`, signify the unchanged code in the file.

The above code is an improvement, but we're still having the gray background "jump-adjust" its height based on if the top-level `li` was being hovered over.

The fix for this is to set the `li` to `position: relative`, and the nested `ul` to `position: absolute`.

This means that we need to update our SCSS file again:
```scss
// positioning //////////////////////////

header {

	&.page-header-wrap {
	}

	nav {

	    &.main-menu-hover-dropdown {
	
			ul {

				li {

					position: relative;

					ul {
						position: absolute;
					}

					&:hover {
						ul {
						}
					}
				}
			}
		}
	}
}
....
```

Now we are finally getting the desired result: The sub-menu group is hidden, and then showing when we hover over its `li` parent element.

However, the nested `ul` doesn't have any background, and thus it doesn't really look like a sub-menu group. We'll fix that by improving the **color** portion of the SCSS file:
```scss
// colors //////////////////////////////

header {

	&.page-header-wrap {
		background: lightgray;	
	}

	nav {

	    &.main-menu-hover-dropdown {
	
			ul {

				li {

					ul {
						background: white;
					}

					&:hover {
						ul {
						}
					}
				}
			}
		}
	}
}
```

While this approach to writing CSS might feel repetitive and redundant at first, consider the following:
{:class="d-block"}
![Collapsable nested SCSS declarations allow us to focus on any important aspect of a given component](/assets/img/main-menu-hover-dropdown/002.png)

Collapsable nested SCSS declarations allow us to focus on any important aspect of a given component. This further reinforces our understanding of best practices and allows us to spot and remember patterns across different components and implementations.

Additionally, such a sturdy structure of our components allows for extensibility and quicker and painless customization.

We get a bunch of customizable CSS-first components, build up to the highest standards of front-end web development.

Now we can add some additional styling to the `ul`:
```scss
ul {
    padding: 1rem;
    top: 2.1rem;
    border: 1px solid gray;
    min-width: max-content;
}
```

Of course, the above code needs to be properly added to our component's SCSS structure, in two different sections.

Here's the first one:
```scss
// display & box model //////////////////
header {

	&.page-header-wrap {

		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}

	nav {

	    &.main-menu-hover-dropdown {
	
			ul {
	
			    display: flex;
    			flex-wrap: wrap;
    			padding-left: 0;

				li {

					padding-right: 1rem;

					&:last-child {

						padding-right: 0;
					}

					ul {
						display: none;
						padding: 1rem;
						top: 2.1rem;
						min-width: max-content;
						border-width: 1px;
						border-style: solid;
					}
...
```

Here's the second one:
```scss
// colors //////////////////////////////
header {

	&.page-header-wrap {
		background: lightgray;	
	}

	nav {

	    &.main-menu-hover-dropdown {
	
			ul {

				li {

					ul {
						background: white;
						border-color: gray;
					}
```

We might think that this is all that it takes, but we actually have a bit more fixes to apply.

The biggest issue we're having here is that a hover on the `li` in the main element will trigger the toggle of the `display` property on the nested `ul`; however, since the `li` area has lower height than the wrapping `nav`, once we try hovering down to the `ul` links, the mouse will no longer stay hovered over the `li`, and thus the `ul` that depends on this hover to be shown - will hide again.

To make the issue more obvious, we can add a background color on the `li` itself, and thus see the content area where the hover will trigger the appearance of the initially hidden `ul`.
```scss
// colors //////////////////////////////
header {

	&.page-header-wrap {
		background: lightgray;	
	}

	nav {

	    &.main-menu-hover-dropdown {
	
			ul {

				li {
						background: gray;
```

Here is the look of the menu now.

{:class="d-block"}
![Our menu after adding the background on top-level li elements](/assets/img/main-menu-hover-dropdown/003.png)

Now we can understand the issue that we're faced with:
* the ul inside the navbar has redundant `margin-block-start` and `margin-block-end` properties set; the solution is to reset all the margins to 0
* we subsequently need to add vertical padding to top level `li` elements on the menu

Additionally, due to the way the CSS inheritance works, **all** the `li` that are nested in a `ul` will also get the background of `gray` - as shown in the above image.

This means that we'll need to increase the specificity on the nested `li` by implementing either one of these two options:
* using the `ul > li` syntax (the direct descendant syntax)
*  


[hover-dropdown]: {{ site.baseurl }}/main-menu-hover-dropdown
[nimble-gh]:   https://github.com/nimblecss/project
[coming-soon]: https://www.nimblecss.com/
