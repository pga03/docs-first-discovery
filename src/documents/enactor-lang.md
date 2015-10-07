---
title: Language Enactor
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.enactor.lang`

**File:** `enactors.js`

Used to set the page's language by 1) saving the selected
language to the settings store and 2) reloading the page. When the page reloads, it will
automatically select the appropriate language based on the saved preference.

## Adding a Language Enactor

The Language Enactor should be bound to an instance of a Preferences Editor by supplying it in
an [Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
fluid.defaults("my.auxSchema", {
    auxiliarySchema: {
        "lang": {
            "type": "gpii.firstDiscovery.language",
            "enactor": {
                "type": "gpii.firstDiscovery.enactor.lang"
            }
        }
    }
});
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the Language Enactor:

* [`fluid.prefs.enactor`](http://docs.fluidproject.org/infusion/development/Enactors.html)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `lang` | The selected language | A valid language code e.g.: `"en-US"`, `"fr-FR"`, `"es-MX"`, `"de-DE"`, `"nl-NL"`, `"sv-SE"`|  `"en-US"` |



## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `reloadPage` | Triggers a page reload. | none |


## Members

| Member   | Description | Values | Default |
|--------|-------------|--------|---------|
| `initialLangSet` | The state whether or not the initial language was set. This is to prevent a page reload on initialization | Boolean |  `false` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/enactors.js"></script>
```
