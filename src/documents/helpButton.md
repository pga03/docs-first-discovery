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

## Using the Help Button

*Option 1*: Typically used as a sub-component of a Preferences Editor Loader,
particularly the [First Discovery Editor](firstDiscoveryEditor.md):
```javascript
helpButton: {
    type: "gpii.firstDiscovery.helpButton",
    container: "{that}.dom.helpButton",
    options: {}
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myHelpButton = gpii.firstDiscovery.helpButton(container, options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)
* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/helpButton.js"></script>
```
