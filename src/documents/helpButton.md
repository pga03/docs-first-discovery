---
title: Help Button
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.helpButton`

**File:** `helpButton.js`

The Help Button provides a component for handling the interface and interaction of help.
This has only been roughed in and currently only sets the text of the help button to
assist with localization.

## Adding a Help Button

*Option 1*: Typically used as a sub-component of a Preferences Editor Loader,
particularly the [First Discovery Editor](firstDiscoveryEditor.md):
```javascript
helpButton: {
    type: "gpii.firstDiscovery.helpButton",
    container: "{that}.dom.helpButton",
    options: {}
}
```

*Option 2*: Adding as a stand alone component:
```javascript
var myHelpButton = gpii.firstDiscovery.helpButton(container, options);
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/helpButton.js"></script>
```
