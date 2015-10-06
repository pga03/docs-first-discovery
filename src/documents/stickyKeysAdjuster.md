---
title: Sticky Keys Adjuster
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.keyboard.stickyKeysAdjuster`

**File:** `stickyKeysAdjuster.js`

Creates the interface for users to experiment the keyboard feature when the sticky key
preference is turned on or off.

## Adding a Sticky Keys Adjuster

*Option 1*: Typically this component is used as a sub-component of the [Sticky Key](keyboard.md) panel:
```javascript
assistance: {
    type: "gpii.firstDiscovery.keyboard.stickyKeysAdjuster",
    container: "{that}.container",
    options: {}
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myStickyKeyAdjuster = gpii.firstDiscovery.keyboard.stickyKeysAdjuster(container, options);
```


## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
* [`gpii.firstDiscovery.attachTooltip`](attachTooltip.md)
* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `stickyKeysEnabled` | Whether or not the sticky key preference is turned on. | Boolean | undefined |
| `tryAccommodation ` |Whether or not the user has chosen to try the sticky key feature.  | Boolean | undefined |

## Supported Events

| Event  | Type |Description | Parameters | Parameter Description |
|--------|------|------------|------------|-----------------------|
| `stickyKeysEnabled` | default |  | `component` |  An instance of `` |
| `tryAccommodation ` | default |  | `number` |   |

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `toggleStickyKeys` | Toggles `model.stickyKeysEnabled` between an enabled/disabled state. | None  |
| `toggleTry` | Toggles `model.tryAccommodation` between an enabled/disabled state. | None  |

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`selectors`</td>
        <td>Javascript object containing selectors for various fragments of the markup, including the containers for the subcomponents.</td>
        <td></td>
        <td>See [Selectors](#selectors) below</td>
    </tr>
</table>

## Selectors

One of the options that can be provided to the First Discovery Editor is a set of CSS-based
selectors identifying where in the DOM different elements can be found. The value for the option
is itself a Javascript object containing name/value pairs:

```javascript
selectors: {
    selector1Name: "selector 1 string",
    selector2Name: "selector 2 string",
      ...
}
```

| Selector Name | Description | Default |
|---------------|-------------|---------|
| `description` | The description of why the sticky key feature is useful. | `".gpiic-fd-keyboard-stickyKeysAdjuster-desc"` |
| `tryButton` | The try it button. | `".gpiic-fd-keyboard-stickyKeysAdjuster-try"` |
| `accommodation` | The wrapper container of elements to operate the sticky key feature. Typically includes these elements: `accommodationInstr`, `accommodationName`, `accommodationState`, `accommodationToggle` | `".gpiic-fd-keyboard-stickyKeysAdjuster-accommodation"` |
| `accommodationInstr` | The description of an example of how to use the sticky key feature. | `".gpiic-fd-keyboard-stickyKeysAdjuster-accommodationInstr"` |
| `accommodationName` | The label of "Sticky Keys". | `".gpiic-fd-keyboard-stickyKeysAdjuster-accommodationName"` |
| `accommodationState` | The current on/off state of the sticky key feature. | `".gpiic-fd-keyboard-stickyKeysAdjuster-accommodationState"` |
| `accommodationToggle` | The button to toggle the on/off state of the sticky key feature. | `".gpiic-fd-keyboard-stickyKeysAdjuster-accommodationToggle"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/navButtons.js"></script>
```

