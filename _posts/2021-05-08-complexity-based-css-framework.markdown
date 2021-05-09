---
layout: post
title:  "Alternative ways of looking at CSS: complexity-based css framework"
date:   2021-05-08 08:28:52 +0200
categories: framework ideas
---

Here's another idea.

How about building a "complexity-based" css framework?

Here's how that would work.

We have several "parameters" whose complexity we can determine based on several factors.

For example, let's say we have an alert component.

For this alert component, there are, say, five levels of complexity that we can have out-of-the box:
* 0, zero, simplest
* 1, one, simple
* 2, two, normal
* 3, three, advanced
* 4, max, complex

But what are we making more or less complex?
* layout (as in how much is it diverging from the normal document flow, with zero being non-diverging, and max being extremly divergent from normal document flow)
* decorations (as in all the little tid-bits, such as borders, shadows, etc, with zero being minimalist, and max being complex)
* skin (with 0 being a neutral theme, and 4 being a glaring theme)
* structure (with 0 being a minimal structure, and 4 being a complex structure - but this is really HTML and doesn't belong here)
* responsive adjustment (with 0 being no change on all breakpoints, and 4 being extreme change across from one breakpoint to another)
* behavior (with 0 being no behavior to 4 being extreme changes in behavior)

Based on all the above mentioned, here's an alert component:
```
<div class="alert layout-one decorations-three responsive-three behavior-zero skin-5">
	<p>This is just an alert for the user.</p>
</div>
```


[nimble-philosophy]: https://www.nimblecss.com/philosophy
[nimble-gh]:   https://github.com/nimblecss/project
[coming-soon]: https://www.nimblecss.com/
