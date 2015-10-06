---
title: Attach Tooltip Renderer
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.attachTooltip.renderer`

**File:** `tooltip.js`

Attach Tooltip - Renderer provides a means for attaching tooltips to various elements in the DOM.
The Attach Tooltip - Renderer grade is not intended to be used on its own, but is
provided as a base grade to another component that will use it's capabilities for binding tooltips.
This is very similar to [Attach Tooltip](attachTooltip.md),
except that it is geared for working with
[fluid.rendererComponent](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)s
where the tooltip model needs to be updated after rendering.

## Adding an Attach Tooltip Renderer to a component/grade

To mixin the Attach Tooltip Renderer into your Component/Grade, supply it as a `gradeNames` option:
```javascript
fluid.defaults("my.component", {
    gradeNames: ["gpii.firstDiscovery.attachTooltip.renderer"]
});```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the Attach Tooltip:

* [`fluid.rendererComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
* [`gpii.firstDiscovery.attachTooltip`](attachTooltip.md)

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
```

