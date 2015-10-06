---
title: Sticky Key Panel – Text To Speech
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.keyboardTts`

**File:** `panels.js`

Adds the self-voicing to read the instructions at the various stages of the
[Sticky Key Panel](keyboard.md) workflow. This component is not intended to be used on its own,
but provided as a grade to the Sticky Key Panel Component. This component also relies on the
availability of a component with the
[fluid.textToSpeech](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html)
grade within the component hierarchy to do the actual speaking.

## Adding a Sticky Key Panel – Text To Speech to a Component/Grade

To mixin the Sticky Key Panel – Text To Speech into your Component/Grade,
supply it as a `gradeNames` option in the [Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
"keyboard": {
    "type": "gpii.firstDiscovery.stickyKeys",
    "panel": {
        "type": "gpii.firstDiscovery.panel.keyboard",
        "container": ".gpiic-fd-prefsEditor-panel-keyboard",
        "gradeNames": ["gpii.firstDiscovery.panel.keyboardTts"],
        "template": "%prefix/keyboard.html",
        "message": "%prefix/keyboard.json"
    }
}}
```


## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `speakStickyKeysState` | Announces whether or not the sticky key preference is turned on. | Object: an instance of gpii.firstDiscovery.panel.keyboardTts; Boolean: the state of the sticky key preference |
| `speakPanelInstructions` | Speaks the panel instruction. | none |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

