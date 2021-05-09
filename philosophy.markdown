---
layout: page
title: Philosophy
permalink: /philosophy/
---

This page explains the motivation and philosophy behind [Nimble CSS](https://www.nimblecss.com/)

## Rules

### 0. Use SCSS to increase readability and understanding

SCSS increases readability and understanding.

Nested SCSS mimics HTML structure - we should use that to our advantage.

### 1. CSS Structure Ordering

Each specific component's HTML structure must be split to the following structure ordering.

// CSS property ordering
// 1. Positioning (position)
	// position: ...
	// z-index: ...
	// top: ...
	// right: ...
// 2. Display & box model (dbm)
	// display: ...
	// overflow: ...
	// box-sizing: ...
	// width: ...
	// height: ...
	// padding: ...
	// border: ...
	// margin: ...
// 3. Color (clr)
	// background
	// color
// 4. Text (txt)
	// font-family
	// font-size
	// line-height
	// text-align
// 5. Other (other)
	// cursor

Inside each individual structure ordering, each property is organized logically.

...

## Motivation

Is there anything fundamentally wrong with today's popular CSS frameworks?

We might argue that there is.

Here are some complaints:
1. Not enough components (example: mega menu)
2. Too much reliance on JavaScript
3. Too much "noise" from css classes, ids, HTML attributes, etc.
4. Slow process of customization
5. No "best practice compliance"
6. Too many unneccesary options

Nimble CSS framework tries to do something completely different.
1. It's not a utility framework (like Tailwind)
2. It's not a component-focused framework (like Bootstrap)

So what is it?

Here's a working definition.

Nimble CSS is a CSS-only framework that:
1. Employs no JavaScript at all.
2. Follows very strict semantic HTML standards
3. Employs a minimalist approach.
4. Is easily skinnable.
5. It strives for having a huge variety of components (an ever-growing list of components)

What does that mean in practice?
1. You will be able to choose out of hundreds of skinnable components - to find your perfect fit.
2. Each component's look depends on just a few classes you add to the **wrapping element** - currently, the body element is what decides **the entire layout's look and feel**.
3. It's the source of best HTML semantic code you can find online

What do you get out of using Nimble CSS framework?
1. Fastest prototyping of all frameworks, period.
2. Fastest skin-switching of all frameworks, period.
3. Completely modular, so you can easily cherry-pick only the parts you need.
4. The most semantic HTML of all available frameworks.
5. Really lean HTML and CSS - we avoid bloat as much as possible.

What follows is a logical layout of how the framework works.

## Styling "interactions" between HTML elements

### Container relationships

Basically, all HTML elements' relationships can be defined as:
1. parent-child relationships
2. sibling relationships

#### 1. Parent-child relationships

Here are the parent-child relationships:
1. Relatively positioned parent, absolutely positioned children
2. to be improved...

#### 2. Sibling relationships

Here are the sibling relationships:
1. inline ("span-like")
2. block ("div-like")

We've divided the framework's styling as follows:
1. `x-` is x-axis "positioning"
2. `y-` is y-axis "positioning"
