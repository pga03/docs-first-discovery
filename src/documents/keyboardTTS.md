---
title: Sticky Keys Panel – Text-to-Speech
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.keyboardTts`

**File:** `panels.js`

Adds the self-voicing to read the instructions at the various stages of the
[Sticky Keys Panel](keyboard.md) workflow. This component is not intended to be used on its own,
but provided as a grade to the Sticky Keys Panel Component. This component also relies on the
availability of a component with the
[fluid.textToSpeech](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html)
grade within the component hierarchy to do the actual speaking.

## Using the Sticky Keys Panel – Text-to-Speech grade

Typically, the Sticky Keys Panel – Text-to-Speech grade is added as an extra grade to the [Sticky Keys Panel](keyboard.md) specification in the [Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

To use the Sticky Keys Panel – Text-to-Speech grade, supply it as a `gradeNames` option
in the [Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

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
}}
```


## Methods

<table>
    <thead>
        <tr><th>Method</th><th>Description</th><th>Parameters</th></tr>
    </thead>
    <tbody>
        <tr>
            <td>`speakStickyKeysState`</td>
            <td>Announces whether or not the sticky keys preference is turned on</td>
            <td>
                <dl>
                    <dd>`that` (object)</dd>
                    <dt>an instance of `gpii.firstDiscovery.panel.keyboardTts`</dt>
                    <dd>`state` (boolean)</dd>
                    <dt>the state of the sticky keys preference</dt>
                </dl>
            </td>
        </tr>
        <tr>
            <td>`speakPanelInstructions`</td>
            <td>Speaks the panel instruction</td>
            <td>none</td>
        </tr>
    </tbody>
</table>

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

