---
title: Captions
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.captions`

**File:** `panels.js`

The Captions panel presents an adjuster that allows the user to adjust the captions preference settings.
The adjuster presents Yes and No buttons that allows users to choose whether they want to see captions when playing videos.

This component uses [Yes/No](yesNo.md)
Panel as a base grade so it has the same component structure as Yes/No Panel
in terms of the model, options, selectors and dependencies.

## Using the Captions Panel

*Option 1*: In the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html),
specify the name of the panel as the `type` property of the `panel` section:
```javascript
"captions": {
    "type": "gpii.firstDiscovery.captions",
    "panel": {
        "type": "gpii.firstDiscovery.panel.captions",
        "container": ".gpiic-fd-prefsEditor-panel-captions",
        "template": "%templatePrefix/yesNo.html",
        "message": "%messagePrefix/captions.json"
    }
}
```

Working in conjunction with the Auxiliary Schema, the type, its default value and range of
the captions preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("gpii.firstDiscovery.schemas.captions", {
    gradeNames: ["fluid.prefs.schemas"],
    schema: {
        "gpii.firstDiscovery.captions": {
            "type": "boolean",
            "default": true
        }
    }
});
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.captions(container, options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.panel.yesNo`](yesNo.md)

