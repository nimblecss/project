---
layout: post
title:  "Alternative ways of looking at CSS: Underlying patterns"
date:   2021-05-07 14:41:52 +0200
categories: framework ideas
---


One of the ideas I had for the direction of where this framework might go was the idea of extracting the commonalities of *all* the websites, not component-wise, but pattern-wise.

I wanted to explore if there are useful underlying conceptual patterns that could be integrated into the framework.

I called this exploration: *Varieties*.

Note: this is just a raw idea, not something that's currently being done in the framework.

# Defining varieties

In the varieties list, we categorize all the ways that elements on the page can be ordered and organized.

These are "sub-patterns" that exist for all the components on any website, and are repeated again and again, be it on forms or in major sections of a website's layout.

## Varieties list

### I PARENT-CHILD RELATIONSHIPS

0. Children STRETCHING patterns:
	* blocks:
		* full-width
		* full-height
		* full-width and height
	* bricks:
		* content-width
		* 10%-width
		* 20%-width
		* 25%-width
		* 33%-width
		* 50%-width
		* 75%-width
		* custom%-width
1. Children CONTAINMENT patterns: 
	* fixed parent 
		* x-overflow
		* y-overflow
	* stretchy parent (stretches its size to accomodate children items)
		* flex wrap or grid in too many ways to be useful to "patternize" - or is it?
	* ellipsis
		* text only(?) one line
		* text only(?) clamp
2. Children INNER ALIGNMENT patterns:
	* x-axis split
		* singles:
			* left (no split, single item)
			* center (no split, single item)
			* right (no split, single item)
		* doubles:
			* balanced [xxxx xxxx]
			* crusoe left [x xxxx]
			* crusoe right [xxxx x]
		* triplets:
			* balanced [xx xx xx]
			* crusoe left [x xxx xxx]
			* crusoe right [xxx xxx x]
		* quadruplets:
			* balanced [xx xx xx xx]
			* crusoe left [x xx xx xx]
			* crusoe right [xx xx xx x]
	* y-axis split
		* singles
			* top
			* center
			* bottom
		* doubles:
			* balanced
				=======
				 xxxxx

				 xxxxx
				=======
			* crusoe top
				=======
				   x
				 xxxxx
				=======
			* crusoe bottom
				=======
				 xxxxx
				   x
				=======
	* both x and y axes:
		* singles: 
				* top-left
				* top-center
				* top-right
				* mid-left 
				* mid-center
				* mid-right
				* bottom-left
				* bottom-center
				* bottom-right	
		* doubles:
			* too many combinations, such as:
				* [top-left bottom-right]
				* [top-left center-center]
				* etc.
				* Note: for obvious reasons, it's not really feasible to incorporate these complex patterns into each of the components of any framework.
3. Children OUTTER alignment patterns:
	* x-axis split
		* singles (on the outside):
			* top
			* right
			* bottom
			* left
		* doubles:
			* balanced x [left right]
			* balanced y [top bottom]
		* to be added...
	
4. Sibling spacing (padding/margins):
	* x axis:
		* no spacing (low spacing)
		* spacing (regular spacing)
		* opposites (high spacing)
	* y axis:
		* no spacing (low spacing)
		* spacing (regular spacing)
		* opposites (high spacing)

### II RESPONSIVE ADJUSTMENTS

In this section of patterns, the focus is on how various children interact on the page based on screen width and height.

3. COLUMN DROP
4. CSS GRID
5. LAYOUT SHIFTER
6. MASONRY
7. OVERHAUL (complete transformation from one breakpoint to another)

Unfortunately, altough all of the above might be a useful and streamlined way to *describe* layouts, it might be the wrong approach to take in building a framework.

[nimble-philosophy]: https://www.nimblecss.com/philosophy
[nimble-gh]:   https://github.com/nimblecss/project
[coming-soon]: https://www.nimblecss.com/
