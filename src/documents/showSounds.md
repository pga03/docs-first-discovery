---
title: Show Sounds
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.showSounds`

**File:** `panels.js`

The Show Sounds panel presents an adjuster that allows the user to adjust the show sounds preference settings.
The adjuster presents Yes and No buttons that allow users to choose whether they want the screen to flash when a sound is played.

This component uses [Yes/No](yesNo.md)
Panel as a base grade so it has the same component structure as Yes/No Panel
in terms of the model, options, selectors and dependencies.

## Using the Show Sounds Panel

*Option 1*: In the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html),
specify the name of the panel as the `type` property of the `panel` section:
```javascript
"showSounds": {
    "type": "gpii.firstDiscovery.showSounds",
    "panel": {
        "type": "gpii.firstDiscovery.panel.showSounds",
        "container": ".gpiic-fd-prefsEditor-panel-showSounds",
        "template": "%templatePrefix/yesNo.html",
        "message": "%messagePrefix/showSounds.json"
    }
}
```

Working in conjunction with the Auxiliary Schema, the type and default value of
the show sounds preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("gpii.firstDiscovery.schemas.showSounds", {
    gradeNames: ["fluid.prefs.schemas"],
    schema: {
        "gpii.firstDiscovery.showSounds": {
            "type": "boolean",
            "default": true
        }
    }
});
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.showSounds(container, options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.panel.yesNo`](yesNo.md)

