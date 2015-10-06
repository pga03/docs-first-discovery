---
title: template
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.enactor.lang`

**File:** `enactors.js`

X.

## Adding a X

To mixin the X into your Component/Grade, supply it as a `gradeNames` option:
```javascript
fluid.defaults("my.component", {
    gradeNames: ["x", "autoInit"],
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

*Option 1*: Typically this component is used as a sub-component of the [Keyboard Input](keyboardInput.md).

Adding as sub-component:
```javascript
keymap: {
    type: "gpii.firstDiscovery.usKeymap"
}
```

*Option 2*: Adding as a stand alone component:
```javascript
var myKeymap = gpii.firstDiscovery.usKeymap(options);
```


## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`fluid.viewRelayComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
* [`gpii.firstDiscovery.attachTooltip`](attachTooltip.md)
* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `` |  |  |   |

## Supported Events

| Event  | Type |Description | Parameters | Parameter Description |
|--------|------|------------|------------|-----------------------|
| `` | default |  | `component` |  An instance of `` |
| `` | default |  | `number` |   |

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `` |  | ``:  |

## Members

| Member   | Description | Values | Default |
|--------|-------------|--------|---------|
| `` |  |  |  `` |


## Subcomponents

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
        <td>``</td>
        <td></td>
        <td></td>
        <td>
        <pre><code></code></pre>
        </td>
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
| `` |  | `"."` |
| `` |  | `"."` |

## Dependencies

```html
<link rel="stylesheet" href="src/lib/infusion/src/lib/normalize/css/normalize.css" />
```

