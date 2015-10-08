---
title: Language and Preferences Editor Connector
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.lang.prefEditorConnection`

**File:** `panels.js`

In the First Discovery Tool,
every preference change causes all panels to re-render so that the changed preference can be
applied to the entire tool.
When the [language](lang.md) panel is re-rendered, it needs to scroll to the correct position
to show the selected language button. However, while the language panel is hidden, this scrolling
would not occur because the button positions are not retrievable. This connector component ensures
the language panel re-renders when the user navigates back to the language panel.

## Adding a Language and Preferences Editor Connector component

To mixin the language and preferences editor connector into the [Language](lang.md) Panel:
```javascript
fluid.defaults("gpii.firstDiscovery.panel.lang", {
    gradeNames: ["fluid.prefs.panel", "{that}.options.prefsEditorConnection", "autoInit"],
    ...
});
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.eventedComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Model

This component supports the following
[model](http://docs.fluidproject.org/infusion/development/tutorial-gettingStartedWithInfusion/ModelComponents.html)
properties:

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `enabled` | Indicates whether the text to speech is enabled. | Boolean | undefined |


## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

