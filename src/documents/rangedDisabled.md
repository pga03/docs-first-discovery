---
title: Ranged Panel - With Disabled Message
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.rangedWithDisabledMsg`

**File:** `panels.js`

The ranged panel - with disabled message component is very similar to [Ranged Panel](ranged.md),
except that
it is able to handle cases when the panel needs to be enabled or disabled. When the panel is
disabled, all the control items in the panel including increase and decrease buttons and the
meter are disabled. In the meantime, a message that explains the disabled state is displayed.
This component is not intended to be used on its own, but provided as a base grade to another
component that will use it's capabilities for creating such panels.

This component uses [Ranged Panel](ranged.md) as a base grade, so it has the same component structure as
that panel in terms of the model and options.

## Using the Ranged Panel - With Disabled Message grade

To use the Ranged Panel - With Disabled Message grade, supply it as a `gradeNames` option in your component definition:
```javascript
fluid.defaults("my.component", {
    gradeNames: ["gpii.firstDiscovery.panel.rangedWithDisabledMsg"],
    ...
});
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.panel.ranged`](ranged.md)

## Methods

The ranged panel - with disabled message component inherits all methods from
[Ranged Panel](ranged.md) component and more:

| Method | Description | Parameters |
|--------|-------------|------------|
| `toggleDisplay` | Enable (or disable) the increase and decrease buttons and show (or hide) the disabled message. | `isEnabled` (boolean)  |


## Selectors

One of the options that can be provided to Infusion components is a set of CSS-based
selectors identifying where in the DOM different elements can be found. Components use a
[DOM Binder](http://docs.fluidproject.org/infusion/development/DOMBinder.html) to access the
named elements.

The value for the option is itself a Javascript object containing name/value pairs:

```javascript
selectors: {
    selector1Name: "selector 1 string",
    selector2Name: "selector 2 string",
      ...
}
```

The ranged panel - with disabled message component has same selectors as [Ranged Panel](ranged.md)
component and more:

| Selector Name | Description | Default |
|---------------|-------------|---------|
| `disabledMsg` | The container to show the disabled message | `".gpiic-fd-range-disabledMsg"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

