---
title: First Discovery Editor
layout: default
category: API
---

## First Discovery Editor Overview

The First Discovery Tool is a type of Preferences Editor designed to be an entry point for users
who are new to customizing a user interface to match their own needs and preferences.
It is intended to inform users of some of the various customization options and allow a user
to create an initial set of preferences that meets their current needs and preferences.

## Adding a First Discovery Editor

The First Discovery Editor should be bound to an instance of a
[Preferences Editor](http://docs.fluidproject.org/infusion/development/PreferencesEditor.html)
by supplying it as the loaderGrade in an
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html).

Adding to an [Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
fluid.defaults("my.auxSchema", {
    auxiliarySchema: {
        "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor"]
    }
});
```

Instantiating the [Preferences Editor](http://docs.fluidproject.org/infusion/development/PreferencesEditor.html):

```javascript
fluid.prefs.create(container, {
    build: {
        gradeNames: ["my.auxSchema"]
    }
};
```
## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`gpii.firstDiscovery.tts.fdHookup`](tts-hookup.md)
* [`fluid.prefs.prefsEditorLoader`](http://docs.fluidproject.org/infusion/development/PreferencesEditor.html)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `currentPanelNum` | The panel currently displayed | Panel ID (Number)|  1 |

## Supported Events

| Event  | Type |Description | Parameters | Parameter Description |
|--------|------|------------|------------|-----------------------|
| `currentPanelNum` | default | Fired when the internal prefsEditor, containing all of panels, is ready. | `component` |  An instance of `fluid.prefs.prefsEditor` |
| `onCreateNav` | default | Fired after onPrefsEditorReady, which is when all of the necessary markup is in place. | `component` |  An instance of `fluid.prefs.prefsEditor` |
| `onPanelShown` | default | Fired each time a panel becomes visible. | `number` |  The panel ID of visible shown panel |

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `showPanel` | Sets the visibility of the panels. The panel which is identified as the current panel in the model is made visible, the reset are hidden. | &nbsp; |


## Subcomponents

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`selfVoicing`</td>
        <td>Specifies the Text-To-Speech engine to use for self voicing.</td>
        <td>[`"gpii.firstDiscovery.selfVoicing"`](selfVoicing.md)</td>
        <td>
        <pre><code>selfVoicing: {
    container: "{that}.dom.selfVoicing",
    createOnEvent: "onPrefsEditorReady",
    type: "gpii.firstDiscovery.selfVoicing",
    options: {
        model: {
            enabled: "{prefsEditor}.model.gpii_firstDiscovery_speak",
            utteranceOpts: {
                lang: "{prefsEditor}.model.gpii_firstDiscovery_language",
                rate: "{prefsEditor}.model.gpii_firstDiscovery_speechRate"
            }
        },
        messageBase: "{messageLoader}.resources.prefsEditor.resourceText"
    }
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`helpButton`</td>
        <td>Specifies the type of help button to use. The current help button is mostly a placeholder, as it only sets the text.</td>
        <td>[`"gpii.firstDiscovery.helpButton"`](helpButton.md)</td>
        <td>
        <pre><code>helpButton: {
    type: "gpii.firstDiscovery.helpButton",
    container: "{that}.dom.helpButton",
    createOnEvent: "onPrefsEditorReady",
    options: {
        messageBase: "{messageLoader}.resources.prefsEditor.resourceText"
    }
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`prefsEditor`</td>
        <td>Specifies the underlying prefs editor used. This is the part that contains all of the adjuster panels.</td>
        <td>[`"fluid.prefs.prefsEditor"`](http://docs.fluidproject.org/infusion/development/PreferencesEditor.html)</td>
        <td>
        <pre><code>prefsEditor: {
    container: "{that}.dom.prefsEditor",
    options: {
        selectors: {
            panel: "{firstDiscoveryEditor}.options.selectors.panel"
        },
        events: {
            onPanelShown: "{firstDiscoveryEditor}.events.onPanelShown"
        },
        listeners: {
            onReady: {
                listener: "{firstDiscoveryEditor}.events.onPrefsEditorReady",
                args: "{firstDiscoveryEditor}"
            },
            onAutoSave: "{that}.saveAndApply",
            "onReset.reload": {
                "this": "location",
                method: "reload",
                args: true
            },
            "onCreate.bindResetShortcut": {
                listener: "gpii.firstDiscovery.keyboardShortcut.bindShortcut",
                args: [
                    "body",
                    gpii.firstDiscovery.keyboardShortcut.key.r,
                    ["ctrlKey", "altKey"],
                    "{that}.reset"
                ]
            }
        },
        autoSave: true,
        connectionGradeForLang: "gpii.firstDiscovery.panel.lang.prefEditorConnection",
        distributeOptions: {
            source: "{that}.options.connectionGradeForLang",
            target: "{that > gpii.firstDiscovery.panel.lang}.options.prefsEditorConnection"
        }
    }
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`nav`</td>
        <td>Specifies the component to use to handle the navigation between panels, and the set of panel icons.</td>
        <td>[`"gpii.firstDiscovery.nav"`](nav.md)</td>
        <td>
        <pre><code>nav: {
    type: "gpii.firstDiscovery.nav",
    container: "{that}.dom.nav",
    createOnEvent: "onCreateNav",
    options: {
        model: {
            currentPanelNum: "{firstDiscoveryEditor}.model.currentPanelNum"
        },
        messageBase: "{messageLoader}.resources.prefsEditor.resourceText",
        styles: "{firstDiscoveryEditor}.options.styles",
        panelTotalNum: "{firstDiscoveryEditor}.panels.length"
    }
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`messageLoader`</td>
        <td>Specifies the component and means for loading in the JSON message bundle files.</td>
        <td>[`"fluid.prefs.resourceLoader"`](http://docs.fluidproject.org/infusion/development/LocalizationInThePreferencesFramework.html)</td>
        <td>
        <pre><code>messageLoader: {
    options: {
        locale: "{prefsEditorLoader}.settings.gpii_firstDiscovery_language"
    }
}</code></pre>
        </td>
    </tr>
</table>

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`defaultLocale`</td>
        <td>The language code to use, for selecting the correct message bundle, when no language has been provided in the preferences.</td>
        <td>A valid language code such as: `"en-US"`, `"fr-FR"`, `"es-MX"`, `"de-DE"`, `"nl-NL"`, `"sv-SE"`</td>
        <td>
        This resolves to "en-US":<br/>
        <pre><code>defaultLocale: {
    expander: {
        funcName: "fluid.get",
        args: [{
            expander: {
                funcName: "fluid.defaults",
                args: ["gpii.firstDiscovery.schemas.language"]
            }
        }, ["schema", "properties", "gpii.firstDiscovery.language", "default"]]
    }
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`tooltipOptions`</td>
        <td>The options to be used by any descendant tooltip components.</td>
        <td></td>
        <td>
        <pre><codetooltipOptions: {
    delay: 0,
    duration: 0,
    position: {
        my: "left bottom",
        at: "right+1 top"
    },
    styles: {
        tooltip: "gpii-fd-tooltip"
    },
    items: ".gpiic-fd-tooltip:not([disabled])"
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`selectors`</td>
        <td>Javascript object containing selectors for various fragments of the markup, including the containers for the subcomponents.</td>
        <td></td>
        <td>See [Selectors](#selectors)</td>
    </tr>
    <tr>
        <td>`styles`</td>
        <td>Specific class names used to achieve the look and feel.</td>
        <td></td>
        <td>
        This resolves to "en-US":<br/>
        <pre><code>styles: {
    active: "gpii-fd-active",
    show: "gpii-fd-show",
    currentPanel: "gpii-fd-current",
    lastPanel: "gpii-fd-lastPanel"
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`modelListeners`</td>
        <td>JavaScript object containing model paths and the listeners that are activated when changes happen to those paths.</td>
        <td>Keys in the object are event names, values are functions or arrays of functions.</td>
        <td>See [Model](#model)</td>
    </tr>
</table>

## Selectors

One of the options that can be provided to the First Discovery Editor is a set of CSS-based
selectors identifying where in the DOM different elements can be found. The value for the option
is itself a Javascript object containing name/value pairs:

```javascript
selectors: {
    selector1Name: "selector 1 string",
    selector2Name: "selector 2 string",
      ...
}
```

| Selector Name | Description | Default |
|---------------|-------------|---------|
| `prefsEditor` | The container to use for the internal prefsEditor; which contains all of the adjuster panels. | `".gpiic-fd-prefsEditor"` |
| `panel` |  Passed down to internal prefsEditor to use as its panel selector. | `".gpiic-fd-prefsEditor-panel"` |
| `selfVoicing` | The container for the selfVoicing subcomponent. | `".gpiic-fd-selfVoicing"` |
| `helpButton` | The container for the help button. | `".gpiic-fd-help"` |
| `nav` | The container for the navigation subcomponent. | `".gpiic-fd-nav"` |

## Dependencies

```html
<link rel="stylesheet" href="src/lib/infusion/src/lib/normalize/css/normalize.css" />
<link rel="stylesheet" href="src/lib/foundation/css/foundation.min.css" />
<link rel="stylesheet" href="src/css/style.css" />
<link rel="stylesheet" type="text/css" href="src/lib/infusion/src/framework/preferences/css/Enactors.css" />
<link rel="stylesheet" type="text/css" href="src/lib/infusion/src/framework/preferences/css/PrefsEditor.css" />

<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/schemas/schemas.js"></script>
<script type="text/javascript" src="src/js/keyboardShortcut.js"></script>
<script type="text/javascript" src="src/js/ttsHookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/selfVoicing.js"></script>
<script type="text/javascript" src="src/js/stickyKeysAssessment.js"></script>
<script type="text/javascript" src="src/js/keyboardInput.js"></script>
<script type="text/javascript" src="src/js/stickyKeysAdjuster.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
<script type="text/javascript" src="src/js/enactors.js"></script>
<script type="text/javascript" src="src/js/navButtons.js"></script>
<script type="text/javascript" src="src/js/navIcons.js"></script>
<script type="text/javascript" src="src/js/helpButton.js"></script>
<script type="text/javascript" src="src/js/stepCount.js"></script>
<script type="text/javascript" src="src/js/nav.js"></script>
<script type="text/javascript" src="src/js/firstDiscoveryEditor.js"></script>
```
