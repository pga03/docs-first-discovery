---
title: Show Sounds
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.showSounds`

**File:** `panels.js`

Allows users to choose whether they want the screen to flash when a sound is played.
This component uses [Yes/No](yesNo.md)
Panel as a base grade so it has the same component structure as Yes/No Panel
in terms of the model, options, selectors and dependencies.

## Adding a Show Sounds Panel to a component/grade

*Option 1*: Typically this component integrated into the First Discovery Tool by
supplying it as a type option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):
```javascript
"showSounds": {
    "type": "gpii.firstDiscovery.showSounds",
    "panel": {
        "type": "gpii.firstDiscovery.panel.showSounds",
        "container": ".gpiic-fd-prefsEditor-panel-showSounds",
        "template": "%prefix/yesNo.html",
        "message": "%prefix/showSounds.json"
    }
}
```

Working in conjunction with the Auxiliary Schema, the type, its default value and range of
the show sounds preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("gpii.firstDiscovery.schemas.showSounds", {
    gradeNames: ["autoInit", "fluid.prefs.schemas"],
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

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the Show Sounds panel:

* [`gpii.firstDiscovery.panel.yesNo`](yesNo.md)

