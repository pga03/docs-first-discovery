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

## Using the Keyboard Input component

*Option 1*: Typically this component is used as a sub-component of a [Sticky Keys Panel](keyboard.md):
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

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.attachTooltip`](attachTooltip.md)
* [`gpii.firstDiscovery.msgLookup`](msgLookup.md)
* [`fluid.viewComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Model

This component supports the following
[model](http://docs.fluidproject.org/infusion/development/tutorial-gettingStartedWithInfusion/ModelComponents.html)
properties:

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `stickyKeysEnabled` | Whether or not the sticky keys feature is enabled | `Boolean` |  `false` |
| `shiftLatched` | Whether or not the SHIFT key is latched | `Boolean` |  `false` |
| `userInput ` | The user input | `String` | `""`  |

## Supported Events

This component supports the following
[events](http://docs.fluidproject.org/infusion/development/InfusionEventSystem.html):

| Event  | Type |Description | Parameters |
|--------|------|------------|------------|
| `shiftKeydown` | default | Fired when the SHIFT key is pressed. | none |
| `keypress` | default | Fired when a key is pressed | `ch` (string): The character associated with the pressed key  |
| `shiftLatchChange ` | default | Fired when the SHIFT is pressed and the sticky keys preference has already been turned on | `that` ([component](http://docs.fluidproject.org/infusion/development/UnderstandingInfusionComponents.html)): An instance of `gpii.firstDiscovery.keyboardInput`  |

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `unlatchShift` | Unlatches the SHIFT | none |
| `updateShiftLatchedClass` | Toggles the css class based on whether or not the SHIFT key is latched | none |
| `clearInput` | Clears the input field. | none |
| `openTooltipIfNotFocused` | Opens the tooltip for the input field even when the input field does not have focus, for example, when the mouse hovers over the input field | none |
| `toggleShiftLatched` | Toggles the latched state of the SHIFT key | none |


## Options

This component can be configured using the following
[options](http://docs.fluidproject.org/infusion/development/ComponentOptionsAndDefaults.html):

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
