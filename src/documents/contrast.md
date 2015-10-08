---
title: Contrast
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.contrast`

**File:** `panels.js`

The contrast panel component provides a means to change the contrast theme of the
First Discovery Tool. Each contrast theme defines its own combination of foreground
and background colors.

## Adding a Contrast Panel to a Component/Grade

*Option 1*: Typically this component integrated into the First Discovery Tool by
supplying it as a type option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):
```javascript
"contrast": {
    "type": "fluid.prefs.contrast",
    "panel": {
        "type": "gpii.firstDiscovery.panel.contrast",
        "container": ".gpiic-fd-prefsEditor-panel-contrast",
        "classnameMap": {"theme": "@contrast.classes"},
        "template": "%templatePrefix/contrast.html",
        "message": "%messagePrefix/contrast.json"
    }
}
```

Working in conjunction with the Auxiliary Schema, the type, its default value and range of
the text size preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("fluid.prefs.schemas.contrast", {
    gradeNames: ["fluid.prefs.schemas"],
    schema: {
        "fluid.prefs.contrast": {
            "type": "string",
            "default": "default",
            "enum": ["default", "bw", "wb", "by", "yb", "lgdg"]
        }
    }
});
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.contrast(container, options);
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the Contrast panel:

* [`fluid.prefs.panel`](http://docs.fluidproject.org/infusion/development/Panels.html)
* [`gpii.firstDiscovery.attachTooltip.renderer`](attachTooltipRenderer.md)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `value` | The selected contrast preference | String | undefined |

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`controlValues`</td>
        <td>An object that contains a "theme" element that determines values assigned to HTML radio buttons.</td>
        <td>Object<br/>The "theme" element: array.</td>
        <td>
        <pre><code>controlValues: {
    choice: ["default", "bw", "wb"]
}</code></pre>
        </td>
    </tr>
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
| `themeRow` | The row of each theme selection. It often contains `themeLabel` and `themeInput`. | `".flc-prefsEditor-themeRow"` |
| `themeLabel` | The label for each theme button | `".flc-prefsEditor-theme-label"` |
| `themeInput` | The `<input>` tag for each theme button | `".flc-prefsEditor-themeInput"` |
| `instructions` | The container to display the panel instruction. | `".gpiic-fd-instructions"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

