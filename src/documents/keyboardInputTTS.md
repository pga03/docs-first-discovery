---
title: Keyboard Input - Text-to-Speech
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.keyboardInputTts`

**File:** `keyboardInput.js`

This component adds the self-voicing to the [Keyboard Input](keyboardInput.md) to announce the input character and
whether the SHIFT key is latched. This component is not intended to be used on its own, but
provided as a base grade to another component. It also relies on the availability of a component
with the [`fluid.textToSpeech`](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html) grade within the component hierarchy to do the actual speaking.

## Using the Keyboard Input - Text-to-Speech grade

*Option 1*: Typically, the Keyboard Input - Text-to-Speech component is added via `keyboardInputGradeNames` option to the [Sticky Keys Panel](keyboard.md) specification in the [Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
"keyboard": {
    "type": "gpii.firstDiscovery.stickyKeys",
    "panel": {
        "type": "gpii.firstDiscovery.panel.keyboard",
        "container": ".gpiic-fd-prefsEditor-panel-keyboard",
        "template": "%templatePrefix/keyboard.html",
        "message": "%messagePrefix/keyboard.json",
        "gradeNames": ["gpii.firstDiscovery.panel.keyboardTts", "gpii.firstDiscovery.panel.keyboard.prefEditorConnection"],
        "keyboardInputGradeNames": ["gpii.firstDiscovery.keyboardInputTts"]
    }
}
```

*Option 2*: To use the Keyboard Input - Text-to-Speech grade directly in the [Keyboard Input](keyboardInput.md),
supply it as a `gradeNames` option in the component definition:
```javascript
keyboardInput: {
    type: "gpii.firstDiscovery.keyboardInput",
    container: "{that}.dom.input",
    options: {
        gradeNames: ["gpii.firstDiscovery.keyboardInputTts"],
        ...
    }
}
```

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `speak` | Queues speech | none  |
| `speakOnFocusMessage` | Speaks the message when the input field gets focus | none  |
| `speakShiftState` | Announces when the SHIFT is latched or unlatched. | none  |


## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/keyboardInput.js"></script>
```

