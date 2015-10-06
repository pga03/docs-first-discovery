---
title: Keyboard Input
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.keyboardInput`

**File:** `keyboardInput.js`

When a character is entered via a keyboard, if the SHIFT key is not latched,
the keyboard input component shows the character itself, otherwise, it shows
the corresponding SHIFT latched character.

## Adding a Keyboard Input

*Option 1*: Typically this component is used as a sub-component of a [Sticky Key Panel](stickyKeyPanel.md):
```javascript
keyboardInput: {
    type: "gpii.firstDiscovery.keyboardInput",
    container: "{that}.dom.input",
    options: {...}
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myKeyboardInput = gpii.firstDiscovery.keyboardInput(container, options);
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
* [`gpii.firstDiscovery.tts.fdHookup`](tts-hookup.md)
* [`fluid.prefs.prefsEditorLoader`](http://docs.fluidproject.org/infusion/development/PreferencesEditor.html)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `stickyKeysEnabled` | Whether or not the sticky key feature is enabled | `Boolean` |  `false` |
| `shiftLatched` | Whether or not the SHIFT key is latched | `Boolean` |  `false` |
| `userInput ` | The user input | `String` | `""`  |

## Supported Events

| Event  | Type |Description | Parameters | Parameter Description |
|--------|------|------------|------------|-----------------------|
| `shiftKeydown` | default | Fired when the SHIFT key is pressed. | None | N/A |
| `keypress` | default | Fired when a key is pressed | `String` | The character associated with the pressed key  |
| `shiftLatchChange ` | default | Fired when the SHIFT is pressed and the sticky key preference has already been turned on | `Component` | An instance of `gpii.firstDiscovery.keyboardInput`  |

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `unlatchShift` | Unlatches the SHIFT | None |
| `updateShiftLatchedClass` | Toggles the css class based on whether or not the SHIFT key is latched | None |
| `clearInput` | Clears the input field. | None |
| `openTooltipIfNotFocused` | Opens the tooltip for the input field even when the input field does not have focus, for example, when the mouse hovers over the input field | None |
| `toggleShiftLatched` | Toggles the latched state of the SHIFT key | None |


## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`styles`</td>
        <td>Specific class names used to achieve the look and feel. Its "shiftLatched" element is to specify the class names applied to the input field when the SHIFT key is latched.</td>
        <td>Object</td>
        <td>
        <pre><code>styles: {
    shiftLatched: "gpii-keyboardInput-shiftLatched"
}</code></pre>
        </td>
    </tr>
</table>

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/keyboardInput.js"></script>
```
