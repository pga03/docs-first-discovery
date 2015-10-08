---
title: Congratulations
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.congratulations`

**File:** `panels.js`

Displays the congratulations message.

## Adding a Congratulations Panel to a Component/Grade

*Option 1*: Typically this component integrated into the First Discovery Tool by
supplying it as a type option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):
```javascript
"congratulations": {
    "type": "gpii.firstDiscovery.congratulations",
    "panel": {
        "type": "gpii.firstDiscovery.panel.congratulations",
        "container": ".gpiic-fd-prefsEditor-panel-congratulations",
        "template": "%templatePrefix/congratulationsTemplate.html",
        "message": "%messagePrefix/congratulations.json"
    }
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.congratulations(container, options);
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the Congratulations panel:

* [`fluid.prefs.panel`](http://docs.fluidproject.org/infusion/development/Panels.html)

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
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
| `message` | The container to display the welcome message. | `".gpiic-fd-welcome-instructions"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

