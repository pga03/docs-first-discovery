---
title: Token Panel
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.token`

**File:** `panels.js`

Used the
[GPII Preferences Server API](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md)
to save preferences that users select in the First Discovery Tool to the server as well as
displaying the server returned token. This token identifies the saved preferences for them to be
applied to other devices.

## Using the Token Panel

*Option 1*: Typically this component integrated into the First Discovery Tool by supplying it as a type option in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):
```javascript
"token": {
    "type": "gpii.firstDiscovery.token",
    "panel": {
        "type": "gpii.firstDiscovery.panel.token",
        "container": ".gpiic-fd-prefsEditor-panel-token",
        "template": "%templatePrefix/token.html",
        "message": "%messagePrefix/token.json"
    }
}
```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.token(container, options);
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.prefs.panel`](http://docs.fluidproject.org/infusion/development/Panels.html)

## Supported Events

This component supports the following
[events](http://docs.fluidproject.org/infusion/development/InfusionEventSystem.html):

<table>
    <thead>
        <tr><th>Event</th><th>Type</th><th>Description</th><th>Parameters</th></tr>
    </thead>
    <tbody>
        <tr>
            <td>`onSuccess`</td>
            <td>default</td>
            <td>Fired when the ajax request to the Preferences Server is successful</td>
            <td>
                <dl>
                    <dd>`data`</dd>
                    <dt>The data returned from the server</dt>
                    <dd>`textStatus`</dd>
                    <dt>A string describing the status</dt>
                    <dd>`jqXHR`</dd>
                    <dt>[The `jqXHR` object](http://api.jquery.com/Types/#jqXHR)</dt>
                </dl>
            </td>
        </tr>
        <tr>
            <td>`onError`</td>
            <td>default</td>
            <td>Fired when the ajax request to the Preferences Server is failed</td>
            <td>
                <dl>
                    <dd>`jqXHR`</dd>
                    <dt>[The `jqXHR` object](http://api.jquery.com/Types/#jqXHR)</dt>
                    <dd>`textStatus`</dd>
                    <dt>A string describing the status</dt>
                    <dd>`errorThrown`</dd>
                    <dt>An optional exception object, if one occurred</dt>
                </dl>
            </td>
        </tr>
    </tbody>
</table>

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `showTokenText` | Displays the server returned token. | A string of token text. |
| `savePrefsToServer` | Sends ajax request to the Preferences Server to save preferences. | none |

## Options

This component can be configured using the following
[options](http://docs.fluidproject.org/infusion/development/ComponentOptionsAndDefaults.html):

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`saveRequestConfig`</td>
        <td>To config the endpoint and method for sending ajax request to the server.</td>
        <td>A object with ajax request configurations</td>
        <td>
        <pre><code>saveRequestConfig: {
    url: "/user",
    method: "POST"
}</code></pre>
        </td>
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
| `message` | The container to display the panel instruction. | `".gpiic-fd-token-message"` |
| `token` |  The textarea to display the server returned token. | `".gpiic-fd-token"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```
