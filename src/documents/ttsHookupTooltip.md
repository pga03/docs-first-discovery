---
title: Text-to-Speech Hookup – Tooltip
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.tts.tooltipHookup`

**File:** `ttsHookup.js`

Text-to-Speech Hookup is a grade containing the configuration necessary to bind an invoker to
the Text-to-Speech engine within the component's
[environment](http://docs.fluidproject.org/infusion/development/Contexts.html).

## Adding a Text-to-Speech Hookup – Tooltip

To mixin the Text-to-Speech Hookup – Tooltip into your Component/Grade, supply it as a `gradeNames` option:
```javascript
fluid.defaults("my.component", {
    gradeNames: ["gpii.firstDiscovery.tts.tooltipHookup"]
});```

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `speak` | Calls the queueSpeech method from the Text-to-Speech engine in the component environment | none |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/ttsHookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
```

