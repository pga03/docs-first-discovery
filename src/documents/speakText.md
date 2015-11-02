---
title: Speak Text
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.speakText`

**File:** `panels.js`

The Speak Text panel presents an adjuster that allows the user to adjust the speak text preference settings.
The adjuster presents Yes and No buttons that allow users to turn on or off the text-to-speech.
When the user chooses, an [enactor](http://docs.fluidproject.org/infusion/development/Enactors.html)
activates or deactivates the First Discovery Tool's [text-to-speech](selfVoicing.md) functionality.

This component uses [Yes/No](yesNo.md)
Panel as a base grade so it has the same component structure as Yes/No Panel
in terms of the model, options, selectors and dependencies.

## Using the Speak Text Panel

*Option 1*: In the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html),
specify the name of the panel as the `type` property of the `panel` section:
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

