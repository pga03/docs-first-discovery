---
title: On-Screen Keyboard
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.onScreenKeyboard`

**File:** `panels.js`

The On-Screen Keyboard panel presents an adjuster that allows the user to adjust the
on-screen keyboard preference settings.
The adjuster presents Yes and No buttons that allow users to choose whether or not they want to use the on-screen keyboard.

This component uses [Yes/No](yesNo.md)
Panel as a base grade so it has the same component structure as Yes/No Panel
in terms of the model, options, selectors and dependencies.

## Using the On-Screen Keyboard Panel

*Option 1:* Typically the On-Screen Keyboard Panel is integrated into the first discovery tool by supplying it as a type option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):
```javascript
"onScreenKeyboard": {
    "type": "gpii.firstDiscovery.onScreenKeyboard",
    "panel": {
        "type": "gpii.firstDiscovery.panel.onScreenKeyboard",
        "container": ".gpiic-fd-prefsEditor-panel-onScreenKeyboard",
        "template": "%templatePrefix/yesNo.html",
        "message": "%messagePrefix/onScreenKeyboard.json"
    }
}```

Working in conjunction with the Auxiliary Schema, the type, its default value and range of
the on-sceen keybaord preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("gpii.firstDiscovery.schemas.onScreenKeyboard", {
    gradeNames: ["fluid.prefs.schemas"],
    schema: {
        "gpii.firstDiscovery.onScreenKeyboard": {
            "type": "boolean",
            "default": true
        }
    }
});
```
*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.onScreenKeyboard(container, options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.panel.yesNo`](yesNo.md)

