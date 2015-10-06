---
title: Navigation Buttons
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.navButtons`

**File:** `navButtons.js`

Provides the back/next buttons for navigating between the panels of the [First Discovery Tool](firstDiscoveryEditor.md).

## Adding a Navigation Buttons Componnet

*Option 1*: Typically this component is used as a sub-component of the [Navigation](nav.md):
```javascript
navButtons: {
    type: "gpii.firstDiscovery.navButtons",
    container: "{that}.dom.navButtons",
    options: {...}
}```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myNavButtons = gpii.firstDiscovery.navButtons(container, options);
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
| `currentPanelNum` | The panel currently displayed. Must be in a range from `options.panelStartNum` to `options.panelTotalNum`. (See [Options](#options) below.) | Panel ID (Number) | undefined |
| `isFirstPanel` | Whether or not the current panel is the first panel | Boolean | undefined |
| `isLastPanel` | Whether or not the current panel is the last panel | Boolean | undefined |

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `setButtonLabels` | Sets the labels and tooltip content for the navigation buttons | |
| `toggleButtonStates` | Toggles an element between an enabled/disabled state | `element`: A jQuery element;  `disabled`: A Boolean value of the disabled state to set |
| `adjustCurrentPanelNum` | Changes the current panel by a specified change amount  | `toChange`: A number |
| `backButtonClicked` | Moves the current panel back one position |  |
| `nextButtonClicked` | Moves the current panel forward one position |  |

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`panelTotalNum`</td>
        <td>The total number of panels that the buttons will be navigating through.</td>
        <td>Number</td>
        <td>
        <pre><code>panelTotalNum: null</code></pre>
        </td>
    </tr>
    <tr>
        <td>`panelStartNum`</td>
        <td>The initial panel. This becomes the lower bound index for which panels can be indexed from</td>
        <td>Number</td>
        <td>
        <pre><code>panelStartNum: 1</code></pre>
        </td>
    </tr>
    <tr>
        <td>`selectors`</td>
        <td>Javascript object containing selectors for various fragments of the markup, including the containers for the subcomponents.</td>
        <td></td>
        <td>See [Selectors](#selectors) below</td>
    </tr>
    <tr>
        <td>`styles`</td>
        <td>Specific class names used to achieve the look and feel</td>
        <td></td>
        <td>
        <pre><code>{
    show: "gpii-fd-show"
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`modelListeners`</td>
        <td>JavaScript object containing model paths and the listeners that are activated when changes happen to those paths</td>
        <td>Keys in the object are event names, values are functions or arrays of functions.</td>
        <td>See [Model](#model) above</td>
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
| `back` | The back button | `"#gpiic-fd-navButtons-back"` |
| `backLabel` | The label for the back button | `".gpiic-fd-navButtons-backLabel"` |
| `next` | The next button | `"#gpiic-fd-navButtons-next"` |
| `nextLabel` | The label for the next button | `".gpiic-fd-navButtons-nextLabel"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/navButtons.js"></script>
```

