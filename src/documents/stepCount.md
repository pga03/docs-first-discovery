---
title: Step Count
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.stepCount`

**File:** `stepCount.js`

Assists to display how many steps users have gone through.

## Adding a Step Count component

*Option 1*: Typically this component is used as a sub-component of the [Navigation](nav.md):
```javascript
stepCount: {
    type: "gpii.firstDiscovery.stepCount",
    container: "{nav}.dom.stepCount",
    options: {}
}
```

*Option 2*: Outside the context of the First Discovery Tool,
developers may wish to create a standalone component:
```javascript
var myStepCount = gpii.firstDiscovery.stepCount(container, options);
```


## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)

## Model

This component supports the following
[model](http://docs.fluidproject.org/infusion/development/tutorial-gettingStartedWithInfusion/ModelComponents.html)
properties:

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `currentPanelNum` | Corresponds to the index of the current panel. | Panel ID (Number) | 0 |


## Options

This component can be configured using the following
[options](http://docs.fluidproject.org/infusion/development/ComponentOptionsAndDefaults.html):

| Name   | Description | Values | Default |
|--------|-------------|--------|---------|
| `panelTotalNum` | The total panel number. | Number | 10 |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/stepCount.js"></script>
```

