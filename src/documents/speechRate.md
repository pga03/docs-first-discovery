---
title: Speech Rate
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.speechRate`

**File:** `panels.js`

Allows users to adjust the speed at which items on the screen are read.
This component uses [Ranged Panel - with Disabled Message ](rangedDisabled.md)
as a base grade so it has the same component structure as that panel
in terms of of the model, options, selectors and dependencies.

## Adding a Speech Rate Panel to a component/grade

*Option 1*: Typically this component integrated into the First Discovery Tool by
supplying it as a type option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):
```javascript
"speechRate": {
    "type": "gpii.firstDiscovery.speechRate",
    "panel": {
        "type": "gpii.firstDiscovery.panel.speechRate",
        "container": ".gpiic-fd-prefsEditor-panel-speechRate",
        "template": "%prefix/rangeWithDisabledMsgTemplate.html",
        "message": "%prefix/speechRate.json",
        "gradeNames": ["gpii.firstDiscovery.panel.speechRate.prefsEditorConnection"]
    }
}
```

Working in conjunction with the Auxiliary Schema, the type, its default value and range of
the text size preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("gpii.firstDiscovery.schemas.speechRate", {
    gradeNames: ["autoInit", "fluid.prefs.schemas"],
    schema: {
        "gpii.firstDiscovery.speechRate": {
            "type": "number",
            "default": 1,
            "minimum": 0.1,
            "maximum": 2, // The spec allows for up to 10, but in chrome 2 seems to be the upper bound.
            "divisibleBy": 0.1
        }
    }
});
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.speechRate(container, options);
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`gpii.firstDiscovery.panel.rangedWithDisabledMessage`](rangedDisabled.md)

