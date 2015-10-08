---
title: US Keymap
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.usKeymap`

**File:** `keyboardInput.js`

Provides methods required for measuring the keyboard input such as the latched SHIFT key and
retrieving the corresponding character when the SHIFT key is latched.
Currently this component only supports the US keyboard layout.

## Adding a US Keymap

*Option 1*: Typically this component is used as a sub-component of the [Keyboard Input](keyboardInput.md):
```javascript
keymap: {
    type: "gpii.firstDiscovery.usKeymap"
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myKeymap = gpii.firstDiscovery.usKeymap(options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.component`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `isShiftEvent` | Whether or not the pressed key is a SHIFT key. | `e`: A [keyboard event object](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent) |
| `isShiftEvent` | Whether or not the given character is a lower case letter. | `ch`: A character |
| `isShiftEvent` | Whether or not the given character has a corresponding character when the SHIFT key is latched. | `ch`: A character |
| `isShiftEvent` | Retrieves the corresponding character when the SHIFT key is latched. | `ch`: A character |


## Dependencies

```html
<link rel="stylesheet" href="src/lib/infusion/src/lib/normalize/css/normalize.css" />
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/keyboardInput.js"></script>
```