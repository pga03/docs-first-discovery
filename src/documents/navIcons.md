---
title: Navigation Icons
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.navIcons`

**File:** `navIcons.js`

Wraps the set of [Navigation Icon](icon.md)s and assists in determining the position of each navigation icon.

## Using the Navigation Icons component

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

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Model

This component supports the following
[model](http://docs.fluidproject.org/infusion/development/tutorial-gettingStartedWithInfusion/ModelComponents.html)
properties:

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `pageNum` | Corresponds to the index of the current panel. | Panel ID (Number) | 0 |
| `iconWidth` | The width of the icon. Used to determine where to scroll to make it visible. | Number (in pixels) | 0 |

## Supported Events

This component supports the following
[events](http://docs.fluidproject.org/infusion/development/InfusionEventSystem.html):

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
        <tr>
            <td>`onSetConfirmedIcon`</td>
            <td>default</td>
            <td>Fired to trigger a specific panel icon to show confirmed state</td>
            <td>
                <dl>
                    <dd>`panelNum`</dd>
                    <dt>the number of the panel whose icon state needs to be set to confirmed</dt>
                </dl>
            </td>
        </tr>
        <tr>
            <td>`onSetActiveIcon`</td>
            <td>default</td>
            <td>Fired to trigger a specific panel icon to show active state</td>
            <td>
                <dl>
                    <dd>`panelNum`</dd>
                    <dt>the number of the panel whose icon state needs to be set to active</dt>
                </dl>
            </td>
        </tr>
    </tbody>
</table>

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `showIconPage` | Scrolls the icon container to make sure the current active icon is visible. | none |

## Subcomponents

This component has the following
[subcomponents](http://docs.fluidproject.org/infusion/development/SubcomponentDeclaration.html):

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
        listeners: {
            "{navIcons}.events.onSetConfirmedIcon": {
                funcName: "{that}.setIconState",
                args: ["isConfirmed", "{arguments}.0"]
            },
            "{navIcons}.events.onSetActiveIcon": {
                funcName: "{that}.setIconState",
                args: ["isActive", "{arguments}.0"]
            }
        },
        modelListeners: {
            "{navIcons}.model.pageNum": {
                listener: "gpii.firstDiscovery.icon.measure",
                args: ["{that}", "{navIcons}.applier", "iconWidth"],
                priority: 10
            },
            "{navIcons}.model.currentPanelNum": {
                listener: "gpii.firstDiscovery.navIcons.updateIconModel",
                args: ["{that}", "{change}.value", "{change}.oldValue"]
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

| Selector Name | Description | Default |
|---------------|-------------|---------|
| `icon` | The set of containers to use the [Navigation Icon](icon.md)s. | `".gpiic-fd-navIcon"` |
| `pager` | The container of the [Navigation Icon](icon.md)s. | `".gpii-fd-navIcon-outer"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/navIcons.js"></script>
```

