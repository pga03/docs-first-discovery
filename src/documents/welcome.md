---
title: Welcome
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.welcome`

**File:** `panels.js`

Displays the welcome message.

## Adding a Welcome Panel to a Component/Grade

*Option 1*: Typically this component integrated into the First Discovery Tool by
supplying it as a type option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):
```javascript
"welcome": {
    "type": "gpii.firstDiscovery.welcome",
    "panel": {
        "type": "gpii.firstDiscovery.panel.welcome",
        "container": ".gpiic-fd-prefsEditor-panel-welcome",
        "template": "%prefix/welcomeTemplate.html",
        "message": "%prefix/welcome.json"
    }
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.welcome(container, options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.prefs.panel`](http://docs.fluidproject.org/infusion/development/Panels.html)

## Options

This component can be configured using the following
[options](http://docs.fluidproject.org/infusion/development/ComponentOptionsAndDefaults.html):

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
| `message` | The container to display the welcome message. | `".gpiic-fd-welcome-instructions"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

