---
title: template
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.enactor.lang`

**File:** `enactors.js`

X.

## Using the X

To mixin the X into your Component/Grade, supply it as a `gradeNames` option:
```javascript
fluid.defaults("my.component", {
    gradeNames: ["x"],
    ...
});
```

The First Discovery Editor should be bound to an instance of a
[Preferences Editor](http://docs.fluidproject.org/infusion/development/PreferencesEditor.html)
by supplying it as the loaderGrade in an
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
fluid.defaults("my.auxSchema", {
    auxiliarySchema: {
        "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor"]
    }
});
```

*Option 1*: Typically this component is used as a sub-component of the [Keyboard Input](keyboardInput.md):
```javascript
keymap: {
    type: "gpii.firstDiscovery.usKeymap"
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myKeymap = gpii.firstDiscovery.usKeymap(options);
```


## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
* [`gpii.firstDiscovery.attachTooltip`](attachTooltip.md)
* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)

## Model

This component supports the following
[model](http://docs.fluidproject.org/infusion/development/tutorial-gettingStartedWithInfusion/ModelComponents.html)
properties:

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `` |  |  |   |

## Supported Events

This component supports the following
[events](http://docs.fluidproject.org/infusion/development/InfusionEventSystem.html):

| Event  | Type |Description | Parameters |
|--------|------|------------|------------|
| `` | default |  | none |
| `` | default |  | none  |

<table>
    <thead>
        <tr><th>Event</th><th>Type</th><th>Description</th><th>Parameters</th></tr>
    </thead>
    <tbody>
        <tr>
            <td>`foo`</td>
            <td>default</td>
            <td></td>
            <td>
                <dl>
                    <dd>`foo`</dd>
                    <dt></dt>
                </dl>
            </td>
        </tr>
    </tbody>
</table>

## Methods

| Method   |Description | Parameters |
|--------|------------|------------|
| ``  |  | `` (type):   |

<table>
    <thead>
        <tr><th>Method</th><th>Description</th><th>Parameters</th></tr>
    </thead>
    <tbody>
        <tr>
            <td>`foo`</td>
            <td></td>
            <td>
                <dl>
                    <dd>`foo`</dd>
                    <dt></dt>
                </dl>
            </td>
        </tr>
    </tbody>
</table>

## Members

| Member   | Description | Values | Default |
|--------|-------------|--------|---------|
| `` |  |  |  `` |


## Subcomponents

This component has the following
[subcomponents](http://docs.fluidproject.org/infusion/development/SubcomponentDeclaration.html):

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>``</td>
        <td></td>
        <td>[`""`](.md)</td>
        <td>
        <pre><code></code></pre>
        </td>
    </tr>
    <tr>
        <td>``</td>
        <td></td>
        <td>[`""`](.md)</td>
        <td>
        <pre><code></code></pre>
        </td>
    </tr>
</table>

## Options

This component can be configured using the following
[options](http://docs.fluidproject.org/infusion/development/ComponentOptionsAndDefaults.html):

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>``</td>
        <td></td>
        <td></td>
        <td>
        <pre><code></code></pre>
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
        <pre><code></code></pre>
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
| `` |  | `"."` |
| `` |  | `"."` |

## Dependencies

```html
<link rel="stylesheet" href="src/lib/infusion/src/lib/normalize/css/normalize.css" />
```

