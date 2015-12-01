---
title: Attach Tooltip
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.attachTooltip`

**File:** `tooltip.js`

Attach Tooltip provides a means for attaching tooltips to various elements in the DOM.
The Attach Tooltip grade is not intended to be used on its own, but provided as a base grade
to another component that will use its capabilities for binding tooltips.

## Using the Attach Tooltip grade

To use the Attach Tooltip grade, supply it as a `gradeNames` option in your component definition:
```javascript
fluid.defaults("my.component", {
    gradeNames: ["gpii.firstDiscovery.attachTooltip"],
    ...
});
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Model

This component supports the following
[model](http://docs.fluidproject.org/infusion/development/tutorial-gettingStartedWithInfusion/ModelComponents.html)
properties:

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `currentSelectedIndex` |The index of the currently selected element  | Number | undefined |

## Subcomponents

This component has the following
[subcomponents](http://docs.fluidproject.org/infusion/development/SubcomponentDeclaration.html):

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`tooltip`</td>
        <td>Specifies the tooltip component to use to create the tooltips.</td>
        <td>`"fluid.tooltip"`</td>
        <td>
        <pre><code>tooltip: {
    type: "fluid.tooltip",
    container: "{attachTooltip}.container",
    options: {
        gradeNames: ["gpii.firstDiscovery.tts.tooltipHookup"],
        model: {
            idToContent: {
                expander: {
                    func: "{that}.getTooltipModel"
                }
            }
        },
        invokers: {
            updateIdToContent: {
                changePath: "idToContent",
                value: {
                    expander: {
                        funcName: "{that}.getTooltipModel"
                    }
                }
            },
            getElementInfo: {
                funcName: "gpii.firstDiscovery.attachTooltip.getElementInfo",
                args: ["{fluid.messageResolver}", "{arguments}.0", "{arguments}.1"]
            },
            getTooltipModel: {
                funcName: "gpii.firstDiscovery.attachTooltip.getTooltipModel",
                // Specifying each elements in the argument list to force them to resolve.
                args: ["{attachTooltip}.dom", "{attachTooltip}.options.tooltipContentMap", "{that}.getElementInfo", "{attachTooltip}"]
            }
        }
    }
}</code></pre>
        </td>
    </tr>
</table>

## Options

This component can be configured using the following
[options](http://docs.fluidproject.org/infusion/development/ComponentOptionsAndDefaults.html):

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`tooltipOptions`</td>
        <td>Options to be passed down to the tooltip subcomponent.</td>
        <td>(see: [fluid.tooltip](https://github.com/fluid-project/infusion/blob/master/src/components/tooltip/js/Tooltip.js))</td>
        <td>
        <pre><code>tooltipOptions: {}</code></pre>
        </td>
    </tr>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`tooltipContentMap`</td>
        <td>Defines the mapping between the names in the selectors block and message bundle for dom elements to have tooltips.

Two methods to define mappings:
<ol>
<li>The direct mapping between one element and one label:

        The left hand side is the name in the selectors block for the element to have the tooltip.<br />

        <strong>Note</strong>: the empty string `""` at the left hand is to reference the component container itself. The right hand side is the name in the message bundle referencing the tooltip content for that element.
<pre><code>{
    "": "containerLabel",
    "back": "backLabel"
}</code></pre>
</li>
<li>The mapping btw one common selector used by multiple DOM elements and their correspondig tooltips.

        This is typically used by defining tooltips for rendered radio buttons or checkboxes. The left hand side is same as method 1 to define the name in the selectors block for elements to have tooltips. The right hand side is an object with two paths: tooltip & tooltipAtSelect. Their values are arrays. "tooltip" array contains names in the message bundle to be shown when mapped elements are not selected. "tooltipAtSelect" contains names when elements are selected. The number of elements in these arrays should be same as the number of elements that the left hand selector is attached to.
<pre><code>"langRow": {
    tooltip: ["label1", "label2"...],
    tooltipAtSelect: ["label1-at-select", "label2-at-select"...]
}</code></pre>
</li>
</ol>
</td>
        <td></td>
        <td>
        <pre><code>tooltipContentMap: {}</code></pre>
        </td>
    </tr>
</table>

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
```

