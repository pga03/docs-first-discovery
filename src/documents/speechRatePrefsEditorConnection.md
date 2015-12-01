---
title: Speech Rate and Preferences Editor Connector
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.speechRate.prefsEditorConnection`

**File:** `panels.js`

The [speech rate](speechRate.md) panel component and the [self voicing](selfVoicing.md) component
control the enabling and disabling of the same preference: text-to-speech.
In the First Discovery Tool, the state of the text-to-speech preference is stored in
`prefsEditor.model.gpii_firstDiscovery_speak`.
This connector component distributes this model value into the speech rate panel component.

## Using the Speech Rate and Preferences Editor Connector component

Typically, the Speech Rate and Preferences Editor Connector component is added as an extra grade to the [Speech Rate Panel](speechRate.md) specification in the [Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
"speechRate": {
    "type": "gpii.firstDiscovery.speechRate",
    "panel": {
        "gradeNames": ["gpii.firstDiscovery.panel.speechRate.prefsEditorConnection"],
        ...
    }
}
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)
* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Model

This component supports the following
[model](http://docs.fluidproject.org/infusion/development/tutorial-gettingStartedWithInfusion/ModelComponents.html)
properties:

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `enabled` | Indicates whether the text-to-speech is enabled. | Boolean | undefined |


## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

