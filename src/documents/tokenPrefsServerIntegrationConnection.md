---
title: Token and Preferences Server Integration Connector
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.token.prefsServerIntegrationConnection`

**File:** `panels.js`

This connector sends a http request to the first discovery server to save user selected preferences when the token panel becomes visible.

## Using the Token and Preferences Server Integration Connector component

Typically the Token and Preferences Server Integration Connector is integrated into the First Discovery Tool by supplying it in an
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
"token": {
    "type": "gpii.firstDiscovery.token",
    "panel": {
        "type": "gpii.firstDiscovery.panel.token",
        "container": ".gpiic-fd-prefsEditor-panel-token",
        "template": "%templatePrefix/token.html",
        "message": "%messagePrefix/token.json",
        "gradeNames": ["gpii.firstDiscovery.panel.token.prefsServerIntegrationConnection"]
    }
}
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.modelComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

