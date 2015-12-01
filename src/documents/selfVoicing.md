---
title: Self Voicing
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.selfVoicing`

**File:** `selfVoicing.js`

Provides a Text-to-Speech engine for vocalizing text.

**Note**: This is will only work in browsers that support the
[SpeechSynthesis API](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html#tts-section).

## Using the Self Voicing component

*Option 1*: Typically this component is used as a sub-component of the Preferences Editor Loader,
particularly the [First Discovery Tool Editor](firstDiscoveryEditor.md):
```javascript
selfVoicing: {
    type: "gpii.firstDiscovery.selfVoicing",
    options: {}
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var mySelfVoicing = gpii.firstDiscovery.selfVoicing(options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.textToSpeech`](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html)
* [`fluid.resolveRootSingle`](http://docs.fluidproject.org/infusion/development/Contexts.html#global-components-fluid-resolveroot-and-fluid-resolverootsingle-)

## Methods

<table>
    <thead>
        <tr><th>Method</th><th>Description</th><th>Parameters</th></tr>
    </thead>
    <tbody>
        <tr>
            <td>`queueSpeech`</td>
            <td>Calls `queueSpeechImpl` if the enabled model value is true or the `force` option value is true.</td>
            <td>
                <dl>
                    <dd>`text` (string)</dd>
                    <dt>The string of text to be voiced</dt>
                    <dd>`options` (Object)</dd>
                    <dt>Any valid speech utterance options (see: [`utteranceOpts`](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html#utteranceopts-option))</dt>
                    <dd>`force` (string)</dd>
                    <dt>If true, force to turn on the self voicing</dt>
                </dl>
            </td>
        </tr>
        <tr>
            <td>`queueSpeechImpl`</td>
            <td>Makes use of the [`fluid.textToSpeech.queueSpeech`](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html#queuespeech) to queue speeches.</td>
            <td>
                <dl>
                    <dd>`text` (string)</dd>
                    <dt>The string of text to be voiced</dt>
                    <dd>`interrupt` (boolean)</dd>
                    <dt>Whether or not to stop the self voicing</dt>
                    <dd>`options` (Object)</dd>
                    <dt>Any valid speech utterance options (see: [`utteranceOpts`](http://docs.fluidproject.org/infusion/development/TextToSpeechAPI.html#utteranceopts-option))</dt>
                </dl>
            </td>
        </tr>
        <tr>
            <td>`clearQueue`</td>
            <td>Empties the queue if the self voicing is disabled (muted).</td>
            <td>none</td>
        </tr>
    </tbody>
</table>

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/selfVoicing.js"></script>
```

