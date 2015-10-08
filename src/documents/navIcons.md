---
title: Navigation Icons
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.navIcons`

**File:** `navIcons.js`

Wraps the set of [Navigation Icon](icon.md)s and assists in determining the position of each navigation icon.

## Adding a Navigation Icons component

*Option 1*: Typically this component is used as a sub-component of the [Navigation](nav.md):
```javascript
navIcons: {
    type: "gpii.firstDiscovery.navIcons",
    container: "{nav}.dom.navIcons",
    options: {}
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myNavIcons = gpii.firstDiscovery.navIcons(container, options);
```


## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the Navigation Icons component:

* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `pageNum` | Corresponds to the index of the current panel. | Panel ID (Number) | 0 |
| `iconWidth` | The width of the icon. Used to determine where to scroll to make it visible. | Number (in pixels) | 0 |

## Supported Events

<table>
    <thead>
        <tr><th>Event</th><th>Type</th><th>Description</th><th>Parameters</th></tr>
    </thead>
    <tbody>
        <tr>
            <td>`onCreateIcon`</td>
            <td>default</td>
            <td>Fired to trigger the creation of each navigation icon</td>
            <td>
                <dl>
                    <dd>`element`</dd>
                    <dt>the DOM element to use as the container for the [Navigation Icon](icon.md)</dt>
                    <dd>`position` (number)</dd>
                    <dt>the position of the [Navigation Icon](icon.md)</dt>
                </dl>
            </td>
        </tr>
    </tbody>
</table>

## Subcomponents

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`icon`</td>
        <td>This is a dynamic component. A new instance is created for each `onCreateIcon` event that is fired.</td>
        <td>[`"gpii.firstDiscovery.icon"`](icon.md)</td>
        <td>
        <pre><code>icon: {
    createOnEvent: "onCreateIcon",
    type: "gpii.firstDiscovery.icon",
    container: "{arguments}.0",
    options: {
        position: "{arguments}.1",
        styles: "{navIcons}.options.styles",
        modelListeners: {
            "{navIcons}.model.currentPanelNum": {
                listener: "gpii.firstDiscovery.navIcons.updateIconModel",
                args: ["{that}", "{change}.value", "{change}.oldValue"]
            },
            "{navIcons}.model.pageNum": {
                listener: "gpii.firstDiscovery.icon.measure",
                args: ["{that}", "{navIcons}.applier", "iconWidth"],
                priority: 10
            }
        }
    }
}</code></pre>
        </td>
    </tr>
</table>

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`pageSize`</td>
        <td>The maximum number of icons to show at a time.</td>
        <td>Number</td>
        <td>
        <pre><code>pageSize: 5</code></pre>
        </td>
    </tr>
    <tr>
        <td>`iconHoles`</td>
        <td>A list of all the panel positions which have no [Navigation Icon](icon.md)s.</td>
        <td>An array of indexes (Number)</td>
        <td>
        <pre><code>iconHoles: [2, 8]</code></pre>
        </td>
    </tr>
    <tr>
        <td>`selectors`</td>
        <td>Javascript object containing selectors for various fragments of the markup, including the containers for the subcomponents.</td>
        <td></td>
        <td>See [Selectors](#selectors) below</td>
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
| `icon` | The set of containers to use the [Navigation Icon](icon.md)s. | `".gpiic-fd-navIcon"` |
| `pager` | The container of the [Navigation Icon](icon.md)s. | `".gpii-fd-navIcon-outer"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/navIcons.js"></script>
```

