---
title: Sticky Keys Assessor
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.keyboard.stickyKeysAssessment`

**File:** `stickyKeysAssessment.js`

Assess whether the user needs the help of the sticky key feature. Currently, the assessor is
simply compare whether the user input string is the same as the expected string.

## Adding a Sticky Keys Assessor

*Option 1*: Typically this component is used as a sub-component of the [Sticky Key](keyboard.md) panel:
```javascript
stickyKeysAssessor: {
    type: "gpii.firstDiscovery.keyboard.stickyKeysAssessment",
    options: {}
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myStickyKeyAssessor = gpii.firstDiscovery.keyboard.stickyKeysAssessment(options);
```


## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the Sticky Keys Assessor component:

* [`fluid.modelComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `offerAssistance` | Whether or not the sticky key feature should be offered. | Boolean | undefined |

## Options

| Name   | Description | Values | Default |
|--------|-------------|--------|---------|
| `requiredInput` | The expected string to be input. | String | `""` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/stickyKeysAssessment.js"></script>
```

