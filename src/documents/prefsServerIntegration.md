---
title: Preferences Server Integration
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.prefsServerIntegration`

**File:** `firstDiscoveryEditor.js`

The Preferences Server Integration grade contains the
configuration necessary to connect the [First Discovery Editor](firstDiscoveryEditor.md) with the
[GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md).
This grade is intended to be added as a base grade to the First Discovery Editor.

## Using the Preferences Server Integration grade

The Preferences Server Integration grade is added to the list of `loaderGrades` in an
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
fluid.defaults("my.auxSchema", {
    auxiliarySchema: {
        "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor", "gpii.firstDiscovery.prefsServerIntegration"]
    }
});
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.modelComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `setLastPanelStyle` | Applies a special class name to the First Discovery Editor container when the current visible panel is the last panel of the First Discovery Tool. | none |

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`styles`</td>
        <td>Specify the class name used to identify that the currently visible panel is the last panel.</td>
        <td></td>
        <td>
        <pre><code>styles: {
    lastPanel: "gpii-fd-lastPanel"
}</code></pre>
        </td>
    </tr>
</table>

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/schemas/schemas.js"></script>
<script type="text/javascript" src="src/js/keyboardShortcut.js"></script>
<script type="text/javascript" src="src/js/ttsHookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/selfVoicing.js"></script>
<script type="text/javascript" src="src/js/stickyKeysAssessment.js"></script>
<script type="text/javascript" src="src/js/keyboardInput.js"></script>
<script type="text/javascript" src="src/js/stickyKeysAdjuster.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
<script type="text/javascript" src="src/js/enactors.js"></script>
<script type="text/javascript" src="src/js/navButtons.js"></script>
<script type="text/javascript" src="src/js/navIcons.js"></script>
<script type="text/javascript" src="src/js/helpButton.js"></script>
<script type="text/javascript" src="src/js/stepCount.js"></script>
<script type="text/javascript" src="src/js/nav.js"></script>
<script type="text/javascript" src="src/js/firstDiscoveryEditor.js"></script>
```
