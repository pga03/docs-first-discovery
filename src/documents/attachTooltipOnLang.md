---
title: Attach Tooltip On Lang
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.lang.attachTooltipOnLang`

**File:** `panels.js`

To use a demands block to apply a special css class to tooltips in the [Language](lang.md) Panel,
the Attach Tooltip on Languge Panel component needs to be attached as a sub-component of the
Language Panel. According to
[Contexts](http://docs.fluidproject.org/infusion/development/Contexts.html), when the context
component of the demands block was the language panel itself, the demands block would also be
applied to all panels rather than the Language Panel only. The Attach Tooltip on Languge Panel
component is acted as another layer of containment to work around this issue.

## Adding an Attach Tooltip On Lang component

Typically, the attach tooltip on language panel component is used as a sub-component of
the [Language](lang.md) Panel.
```javascript
fluid.defaults("gpii.firstDiscovery.panel.lang", {
    components: {
        attachTooltipOnLang: {
            type: "gpii.firstDiscovery.panel.lang.attachTooltipOnLang",
            container: ...,
            options: {
                ...
            }
        }
    }
});
```


## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the Attach Tooltip On Lang:

* [`gpii.firstDiscovery.attachTooltip`](attachTooltip.md)


## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

