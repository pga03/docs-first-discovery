---
title: Language
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.lang`

**File:** `panels.js`

The Language panel presents an adjuster that allows the user to adjust the language preference settings.

Used to set the page's language. Currently this action is performed by saving the selected
language to the settings store and reloading the page.

## Using the Language Panel

*Option 1*: In the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html),
specify the name of the panel as the `type` property of the `panel` section:
```javascript
"lang": {
    "type": "gpii.firstDiscovery.language",
    "panel": {
        "type": "gpii.firstDiscovery.panel.lang",
        "container": ".gpiic-fd-prefsEditor-panel-lang",
        "template": "%templatePrefix/lang.html",
        "message": "%messagePrefix/lang.json",
        "stringArrayIndex": {
            "lang": ["lang-en-US", "lang-fr-FR", "lang-es-MX", "lang-de-DE", "lang-nl-NL", "lang-sv-SE"],
            "tooltip": ["lang-en-US-tooltip", "lang-fr-FR-tooltip", "lang-es-MX-tooltip", "lang-de-DE-tooltip", "lang-nl-NL-tooltip", "lang-sv-SE-tooltip"],
            "tooltipAtSelect": ["lang-en-US-tooltipAtSelect", "lang-fr-FR-tooltipAtSelect", "lang-es-MX-tooltipAtSelect", "lang-de-DE-tooltipAtSelect", "lang-nl-NL-tooltipAtSelect", "lang-sv-SE-tooltipAtSelect"]
        }
    }
}
```

Working in conjunction with the Auxiliary Schema, the type, its default value and range of
the language preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):
```javascript
fluid.defaults("gpii.firstDiscovery.schemas.language", {
    gradeNames: ["fluid.prefs.schemas"],
    schema: {
        "gpii.firstDiscovery.language": {
            "type": "string",
            "default": "en-US",
            "enum": ["en-US", "fr-FR", "es-MX", "de-DE", "nl-NL", "sv-SE"]
        }
    }
});
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.lang(container, options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`gpii.firstDiscovery.attachTooltip.renderer`](attachTooltipRenderer.md)
* [`fluid.prefs.panel`](http://docs.fluidproject.org/infusion/development/Panels.html)

## Model

This component supports the following
[model](http://docs.fluidproject.org/infusion/development/tutorial-gettingStartedWithInfusion/ModelComponents.html)
properties:

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `lang` | The language applied to the First Discovery Tool | String | undefined |
| `selectedLang` | The language code that its corresponding button has focus | String | undefined |
| `viewportFirstLangIndex` | The index of the first visible language button | Number | 0 |
| `atStartOfLangs` | Whether the first language button has focus | Boolean | false |
| `atEndOfLangs` | Whether the last language button has focus | Boolean | false |

## Options

This component can be configured using the following
[options](http://docs.fluidproject.org/infusion/development/ComponentOptionsAndDefaults.html):

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`numOfLangPerPage`</td>
        <td>The number of language buttons to be displayed on the panel.</td>
        <td>Number</td>
        <td>
        <pre><code>numOfLangPerPage: 3</code></pre>
        </td>
    </tr>
    <tr>
        <td>`selectors`</td>
        <td>Javascript object containing selectors for various fragments of the markup, including the containers for the subcomponents.</td>
        <td></td>
        <td>See [Selectors](#selectors) below</td>
    </tr>
</table>

## Selectors

One of the options that can be provided to Infusion components is a set of CSS-based
selectors identifying where in the DOM different elements can be found. Components use a
[DOM Binder](http://docs.fluidproject.org/infusion/development/DOMBinder.html) to access the
named elements.

The value for the option is itself a Javascript object containing name/value pairs:

```javascript
selectors: {
    selector1Name: "selector 1 string",
    selector2Name: "selector 2 string",
      ...
}
```

| Selector Name | Description | Default |
|---------------|-------------|---------|
| `instructions` | The container to display the panel instruction. | `".gpiic-fd-lang-instructions"` |
| `langRow` | The row of each language selection. It often contains `langLabel` and `langInput`. | `".gpiic-fd-lang-langRow"` |
| `langLabel` | The label for each language button | `".gpiic-fd-lang-langLabel"` |
| `controlsDiv` | The `<input>` tag for each language button | `".gpiic-fd-lang-controls"` |
| `prev` | The "previous" button | `".gpiic-fd-lang-prev"` |
| `next` | The "next" button | `".gpiic-fd-lang-next"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```

