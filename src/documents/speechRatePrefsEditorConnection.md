---
title: Speech Rate and Preferences Editor Connector
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.speechRate.prefsEditorConnection`

**File:** `panels.js`

X.

## Adding a Speech Rate and Preferences Editor Connector component

Typically passed into the [speech rate](speechRate.md) component by supplying it as a
`gradeNames` option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
"speechRate": {
    "type": "gpii.firstDiscovery.speechRate",
    "panel": {
        "gradeNames": ["gpii.firstDiscovery.panel.speechRate.prefsEditorConnection"],
        ...
    }
}
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `enabled` | Indicates whether the text to speech is enabled. | Boolean | undefined |


## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

