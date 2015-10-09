---
title: Speak Text
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.speakText`

**File:** `panels.js`

Allows users to turn on/off the text to speech. This component uses [Yes/No](yesNo.md)
Panel as a base grade so it has the same component structure as Yes/No Panel
in terms of the model, options, selectors and dependencies.

## Adding a Speak Text Panel to a component/grade

*Option 1*: Typically this component integrated into the First Discovery Tool by
supplying it as a type option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):
```javascript
"speakText": {
    "type": "gpii.firstDiscovery.speak",
    "panel": {
        "type": "gpii.firstDiscovery.panel.speakText",
        "container": ".gpiic-fd-prefsEditor-panel-speakText",
        "template": "%templatePrefix/yesNo.html",
        "message": "%messagePrefix/speakText.json"
    }
}```

Working in conjunction with the Auxiliary Schema, the type, its default value and range of
the speak text preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("gpii.firstDiscovery.schemas.speak", {
    gradeNames: ["fluid.prefs.schemas"],
    schema: {
        "gpii.firstDiscovery.speak": {
            "type": "boolean",
            "default": true
        }
    }
});
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.speakText(container, options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.panel.yesNo`](yesNo.md)

