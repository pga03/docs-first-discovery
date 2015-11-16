---
title: Text-to-Speech Hookup – Preferences Editor
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.tts.prefsEditor`

**File:** `ttsHookup.js`

Text-to-Speech Hookup - First Discovery is a grade containing the configuration necessary to setup the utterance of the panel introductions. As a panel is made visible, a message is uttered. The 'h' key is also wired up utter the panel instructions. This grade is intended to be added as a base grade to the `prefsEditor` subcomponent in the [First Discovery Editor](firstDiscoveryEditor.md).

**Note**: The utterance will only occur when self voicing is enabled.

## Using the Text-to-Speech Hookup – Preferences Editor grade

To use the Text-to-Speech Hookup – Preferences Editor grade, supply it as a `gradeNames` option in your component definition:
```javascript
fluid.defaults("my.component", {
    gradeNames: ["gpii.firstDiscovery.tts.prefsEditor"]
});
```

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `speakPanelMessage` | Utters the panel message. Typically a combination of the step ( e.g. x of y ) and the panel instructions | `speakOpts`: Any valid speech utterance options (see: [utteranceOpts](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html#utteranceopts-option)) |
| `speakPanelInstructions` | Utters the panel instructions | `speakOpts`: Any valid speech utterance options (see: [utteranceOpts](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html#utteranceopts-option)) |

## Options

This component can be configured using the following
[options](http://docs.fluidproject.org/infusion/development/ComponentOptionsAndDefaults.html):

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`panelInstructionsSelector`</td>
        <td>The class name that is added to containers whose instructions need to be uttered.</td>
        <td>A string of a class name</td>
        <td>`".gpiic-fd-instructions"`</td>
    </tr>
</table>

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/ttsHookup.js"></script>
```

