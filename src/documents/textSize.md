---
title: Text Size
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.textSize`

**File:** `panels.js`

Allows users to adjust the text to the size they want. This component uses [Ranged](ranged.md)
Panel as a base grade so it has the same component structure as Ranged Panel
in terms of the model, options, selectors and dependencies.

## Adding a Text Size Panel to a component/grade

*Option 1*: Typically this component integrated into the First Discovery Tool by
supplying it as a type option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):
```javascript
"textSize": {
    "type": "fluid.prefs.textSize",
    "panel": {
        "type": "gpii.firstDiscovery.panel.textSize",
        "container": ".gpiic-fd-prefsEditor-panel-size",
        "template": "%prefix/rangeTemplate.html",
        "message": "%prefix/textSize.json"
    }
}
```

Working in conjunction with the Auxiliary Schema, the type, its default value and range of
the text size preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("gpii.firstDiscovery.schemas.textSize", {
    gradeNames: ["autoInit", "fluid.prefs.schemas"],
    schema: {
        "fluid.prefs.textSize": {
            "type": "number",
            "default": 1,
            "minimum": 0.2,
            "maximum": 1.2,
            "divisibleBy": 0.1
        }
    }
});
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.textSize(container, options);
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the Text Size panel:

* [`gpii.firstDiscovery.panel.ranged`](ranged.md)

