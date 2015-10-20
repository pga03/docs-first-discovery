---
title: Text Size
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.textSize`

**File:** `panels.js`

The Text Size panel presents an adjuster that allows the user to adjust the text size preference settings.
The adjuster presents plus and minus buttons, and a range indicator.
When the user activates the buttons to change the text size, an
[enactor](http://docs.fluidproject.org/infusion/development/Enactors.html)
(provided by the
[Infusion Preferences Framework](http://docs.fluidproject.org/infusion/development/PreferencesFramework.html))
applies the new text size to the First Discovery Tool interface.

This component uses [Ranged](ranged.md)
Panel as a base grade so it has the same component structure as Ranged Panel
in terms of the model, options, selectors and dependencies.

## Using Text Size Panel

*Option 1*: In the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html),
specify the name of the panel as the `type` property of the `panel` section:
```javascript
"textSize": {
    "type": "fluid.prefs.textSize",
    "panel": {
        "type": "gpii.firstDiscovery.panel.textSize",
        "container": ".gpiic-fd-prefsEditor-panel-size",
        "template": "%templatePrefix/rangeTemplate.html",
        "message": "%messagePrefix/textSize.json"
    }
}
```

Working in conjunction with the Auxiliary Schema, the type, its default value and range of
the text size preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("gpii.firstDiscovery.schemas.textSize", {
    gradeNames: ["fluid.prefs.schemas"],
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

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.panel.ranged`](ranged.md)

