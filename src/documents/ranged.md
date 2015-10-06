---
title: Ranged Panel
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.ranged `

**File:** `panels.js`

The ranged panel component provides a means to create panels that adjust a value by clicking DOM
elements such as buttons, as well as showing the adjusted value in a meter. The ranged panel
component is not intended to be used on its own, but provided as a base grade to another component
that will use it's capabilities for creating such panels. An UI example of one of these panels:

![vertical bar with "fast" above it and "slow" below it, with plus and minus buttons next to it](images/rangedPanel.jpeg)

## Adding a Ranged Panel to a component/grade

To mixin the Ranged Panel into your Component/Grade, supply it as a `gradeNames` option:
```javascript
fluid.defaults("my.component", {
    gradeNames: ["gpii.firstDiscovery.panel.ranged"],
    ...
});
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`fluid.prefs.panel`](http://docs.fluidproject.org/infusion/development/Panels.html)
* [`gpii.firstDiscovery.attachTooltip.renderer`](attachTooltipRenderer.md)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `value` | The selected value of the ranged component | Number | undefined  |

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `stepUp` |Increases the model `value` by the step provided in component options  | none  |
| `stepDown` | Decreases the model `value` by the step provided in component options | none  |
| `updateMeter` | Updates the meter DOM element to show the current model `value` | none  |

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`range`</td>
        <td>An object that contains two elements: "min" and "max". They determine the minimum and maximum values of the range.</td>
        <td>Object<br/>"min" and "max" values are numbers.</td>
        <td>
        <pre><code>range: {
    min: 1,
    max: 2
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`step`</td>
        <td>Determines the size or amount of each interval or step the slider takes between the min and max</td>
        <td>Number</td>
        <td>
        <pre><code>step: 0.1</code></pre>
        </td>
    </tr>
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
| `rangeInstructions` | The panel instruction. | `".gpiic-fd-range-disabledMsg"` |
| `controls` | The wrapper container for all control items listed below | `".gpiic-fd-range-controls"` |
| `meter` |The meter that shows the selected value  | `".gpiic-fd-range-indicator"` |
| `max` | The container to display the label for the maximum value, such as "fast" | `".gpiic-fd-range-max"` |
| `min` | The container to display the label for the minimum value, such as "slow" | `".gpiic-fd-range-min"` |
| `increase` | The DOM element that triggers the increase of the selected value by clicking it | `".gpiic-fd-range-increase"` |
| `decrease` | The DOM element that triggers the decrease of the selected value by clicking it | `".gpiic-fd-range-decrease"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

