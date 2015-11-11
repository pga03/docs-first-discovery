---
title: Language and Preferences Editor Connector
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.lang.prefEditorConnection`

**File:** `panels.js`

In the First Discovery Tool,
every preference change causes all panels to re-render so that the changed preference can be
applied to the entire tool.
When the [language](lang.md) panel is re-rendered, it needs to scroll to the correct position
to show the selected language button. However, while the language panel is hidden, this scrolling
would not occur because the button positions are not retrievable. This connector component ensures
the language panel re-renders when the user navigates back to the language panel.

## Using the Language and Preferences Editor Connector component

Typically, the Language and Preferences Editor Connector is added as an extra grade to the [Language Panel](lang.md) specification in the [Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
"lang": {
    "type": "gpii.firstDiscovery.language",
    "panel": {
        "type": "gpii.firstDiscovery.panel.lang",
        "container": ".gpiic-fd-prefsEditor-panel-lang",
        "template": "%templatePrefix/lang.html",
        "message": "%messagePrefix/lang.json",
        "gradeNames": ["gpii.firstDiscovery.panel.lang.prefEditorConnection"]
    }
}
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.component`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

