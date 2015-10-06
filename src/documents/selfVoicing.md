---
title: Self Voicing
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.selfVoicing`

**File:** `selfVoicing.js`

Provides both a Text-To-Speech engine for vocalizing text and user interface for
enabling/disabling (mute/unmute) the speech synthesis.

Note: This is will only work in browsers that support the
[SpeechSynthesis API](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html#tts-section).

## Adding a Self Voicing component


*Option 1*: Typically this component is used as a sub-component of the Preferences Editor Loader,
particularly the [First Discovery Tool Editor](firstDiscoveryEditor.md):
```javascript
selfVoicing: {
    type: "gpii.firstDiscovery.selfVoicing",
    container: "{that}.dom.selfVoicing",
    options: {}
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var mySelfVoicing = gpii.firstDiscovery.selfVoicing(container, options);
```


## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the Self Voicing component:

* [`gpii.firstDiscovery.attachTooltip`](attachTooltip.md)
* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)
* [`fluid.textToSpeech`](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html)

## Model

<table>
    <tr><th>Path</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`enabled`</td>
        <td>The enabled/disabled (unmute/mute) state of the component</td>
        <td>true/false (Boolean)</td>
        <td>false</td>
    </tr>
    <tr>
        <td>`utteranceOpts`</td>
        <td>The utterance options to use for all utterances, unless overridden in queueSpeech call</td>
        <td>An object containing any of the following:
            <ul>
                <li>text: text to synthesize, should be avoided</li>
                <li>lang: the language of the synthesized text</li>
                <li>voiceURI: a url pointing at a voice synthesizer</li>
                <li>volume: a value between 0 and 1</li>
                <li>rate: speech rate, value between 0.1 and 10</li>
                <li>pitch: speech pitch, value between 0 and 2</li>
            </ul>
        </td>
        <td>`{}`</td>
    </tr>
</table>

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `queueSpeech` |Makes use of the fluid.textToSpeech.queueSpeech but only calls it if the enabled model value is true. It also prevents the speech from actually queue, and sets it to always interrupt.  |`text`: The string of text to be voiced; `options`: Any valid speech utterance options (see: [`utteranceOpts`](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html#utteranceopts-option))  |
| `toggleState` | Toggles the enabled state, effectively muting/unmuting. |   |
| `setLabel` |Sets the mute button label depending on the enabled  state. Note: this is meant for internal use by the component and not for external API calls.  |   |
| `setTooltip` | Sets the tooltip for the mute button depending on the enabled  state. Note: this is meant for internal use by the component and not for external API calls. |   |
| `setMuteStyle` | Sets the style class on the mute button depending on the enabled  state. Note: this is meant for internal use by the component and not for external API calls. |   |
| `clearQueue` | Empties the queue if the self voicing is disabled (muted). |   |
| `speakVoiceSate` | Utters the current enabled  state. | `options`: Any valid speech utterance options (see: [`utteranceOpts`](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html#utteranceopts-option))  |

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`tooltipContentMap`</td>
        <td>The mapping between the selector and tooltip message to be displayed (See [Attach Tooltip](attachTooltip.md)).</td>
        <td></td>
        <td>
        <pre><code>tooltipContentMap: {
    "mute": "mutedTooltip"
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`selectors`</td>
        <td>Javascript object containing selectors for various fragments of the markup, including the containers for the subcomponents.</td>
        <td></td>
        <td>See [Selectors](#selectors) below</td>
    </tr>
    <tr>
        <td>`styles`</td>
        <td>Specific class names used to achieve the look and feel</td>
        <td></td>
        <td>
        <pre><code>styles: {
    muted: "gpii-fd-selfVoicing-muted",
    unmuted: "gpii-fd-selfVoicing-unmuted"
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`modelListeners`</td>
        <td>JavaScript object containing model paths and the listeners that are activated when changes happen to those paths</td>
        <td>Keys in the object are event names, values are functions or arrays of functions.</td>
        <td>See [Model](#model) above</td>
    </tr>
</table>

## Selectors

One of the options that can be provided to the First Discovery Editor is a set of CSS-based
selectors identifying where in the DOM different elements can be found. The value for the option
is itself a Javascript object containing name/value pairs:

```javascript
selectors: {
    selector1Name: "selector 1 string",
    selector2Name: "selector 2 string",
      ...
}
```

| Selector Name | Description | Default |
|---------------|-------------|---------|
| `mute` | The DOM element to use as the mute button | `".gpiic-fd-selfVoicing-mute"` |
| `muteLabel` | The DOM element to use as the label for the mute button | `".gpiic-fd-selfVoicing-muteLabel"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/selfVoicing.js"></script>
```

