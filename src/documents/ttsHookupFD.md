---
title: Text-to-Speech Hookup – First Discovery
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.tts.fdHookup`

**File:** `ttsHookup.js`

Text-to-Speech Hookup - First Discovery is a grade containing the configuration necessary
to setup the utterance of the panel introductions. As a panel is made visible,
a message is uttered. The 'h' key is also wired up utter the panel instructions.
This grade is intended to be added as a base grade to the
[First Discovery Editor](firstDiscoveryEditor.md).

Note: _The utterance will only occur when self voicing is enabled._

## Adding a Text-to-Speech Hookup – First Discovery

To mixin the Text-to-Speech Hookup – First Discovery into your Component/Grade, supply it as a `gradeNames` option:
```javascript
fluid.defaults("my.component", {
    gradeNames: ["gpii.firstDiscovery.tts.fdHookup"]
});```

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `speakPanelMessage` | Utters the panel message. Typically a combination of the step ( e.g. x of y ) and the panel instructions | `speakOpts`: Any valid speech utterance options (see: [utteranceOpts](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html#utteranceopts-option)) |
| `speakPanelInstructions` | Utters the panel instructions | `speakOpts`: Any valid speech utterance options (see: [utteranceOpts](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html#utteranceopts-option) |

## Subcomponents

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`selfVoicing`</td>
        <td>Specifies the Text-To-Speech engine to use for self voicing. This provides additional configuration on top of what is specified in [gpii.firstDiscovery.firstDiscoveryEditor](firstDiscoveryEditor.md).</td>
        <td></td>
        <td>
        <pre><code>selfVoicing: {
    options: {
        invokers: {
            speakPanelMessage: {
                funcName: "gpii.firstDiscovery.tts.fdHookup.speakPanelMessage",
                args: ["{firstDiscoveryEditor}", "{that}.msgLookup.stepCountMsg", "{that}.msgLookup.panelMsg", "{that}.queueSpeech", "{arguments}.0"]
            },
            speakPanelInstructions: {
                funcName: "gpii.firstDiscovery.tts.fdHookup.speakPanelInstructions",
                args: ["{firstDiscoveryEditor}", "{that}.queueSpeech", "{arguments}.0"]
            }
        },
        listeners: {
            "onCreate.bindKeypress": {
                listener: "gpii.firstDiscovery.keyboardShortcut.bindShortcut",
                args: ["body", gpii.firstDiscovery.keyboardShortcut.key.h, [], "{that}.speakPanelInstructions"]
            }
        },
        modelListeners: {
            "{firstDiscoveryEditor}.model.currentPanelNum": "{that}.speakPanelMessage"
        }
    }
}</code></pre>
        </td>
    </tr>
</table>

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/ttsHookup.js"></script>
```

