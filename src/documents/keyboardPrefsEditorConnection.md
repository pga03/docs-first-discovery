---
title: Sticky Keys Panel and Preferences Editor Connector
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.keyboard.prefEditorConnection`

**File:** `panels.js`

The First Discovery Tool keeps track of the operations on the sticky key panel so that users' last operation can be restored when they are back to the tool. Users can use a shortcut key (CTRL + ALT + r) to restore the tool to its initial fresh state. In order to reset the sticky key panel to its initial state, the model path `offerAssistance` needs to be deleted from `gpii.firstDiscovery.panel.keyboard` model since the present of this model path, regardless of its value, triggers an intermediate sticky key panel page to be rendered.

The Sticky Keys Panel and Preferences Editor Connector is intended to be added as a base grade to `gpii.firstDiscovery.panel.keyboard` to delete the model path `offerAssistance` from the `gpii.firstDiscovery.panel.keyboard` instance.

## Using the Sticky Keys Panel and Preferences Editor Connector component

Typically, the Sticky Keys Panel and Preferences Editor Connector is added as an extra grade to the [Sticky Keys Panel](keyboard.md) specification in the [Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
"keyboard": {
    "type": "gpii.firstDiscovery.stickyKeys",
    "panel": {
        "type": "gpii.firstDiscovery.panel.keyboard",
        "container": ".gpiic-fd-prefsEditor-panel-keyboard",
        "template": "%templatePrefix/keyboard.html",
        "message": "%messagePrefix/keyboard.json",
        "gradeNames": ["gpii.firstDiscovery.panel.keyboardTts", "gpii.firstDiscovery.panel.keyboard.prefEditorConnection"]
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

