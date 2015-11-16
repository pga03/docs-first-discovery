---
title: Message Lookup
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.msgLookup`

**File:** `msgLookup.js`

The Message Lookup provides a means for resolving
[message bundles](http://docs.fluidproject.org/infusion/development/LocalizationInThePreferencesFramework.html)
and accessing individual messages via
[IoC expressions](http://docs.fluidproject.org/infusion/development/IoCReferences.html).
Message bundles are the localization strategy used by the
[Preferences Framework](http://docs.fluidproject.org/infusion/development/PreferencesFramework.html),
and should contain all the strings used by a user interface. As such, Message Lookup components
are not intended to be used on their own, but provided as a grade to another component that will
use its capabilities for displaying messages/strings to a user.

## Using the Message Lookup grade

To use the Message Lookup grade, supply it as a `gradeNames` option in your component definition:

```javascript
fluid.defaults("my.component", {
    gradeNames: ["gpii.firstDiscovery.msgLookup"],
    ...
});
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* `fluid.presf.msgLookup`

## Subcomponents

This component has the following
[subcomponents](http://docs.fluidproject.org/infusion/development/SubcomponentDeclaration.html):

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`msgResolver`</td>
        <td>Specifies the type of message resolver to use for resolving the messages from a message bundle</td>
        <td>`"fluid.messageResolver"`</td>
        <td>
        <pre><code>msgResolver: {
    type: "fluid.messageResolver"
}</code></pre>
        </td>
    </tr>

</table>

## Options

This component can be configured using the following
[options](http://docs.fluidproject.org/infusion/development/ComponentOptionsAndDefaults.html):

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`messageBase`</td>
        <td>

Javascript object containing messages available for the component to output/display. Typically this will be the contents fetched from a message bundle (JSON file).</td>
        <td>Any valid key/value pairing, where the value is a localized string. The key could also take a namespace by providing a prefix (e.g. namespace-key). This allows for grouping strings to be accessed as an array of strings.
        <pre><code>messageBase: {
    "someMessage": "a localized message",
    "myNamespace-string1": "The first localized string",
    "myNamespace-string2": "The second localized string"
}</code></pre></td>
        <td>
        <pre><code>messageBase: {}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`stringArrayIndex`</td>
        <td>Works in conjunction with namespaced message bundle keys to provide an array of strings.</td>
        <td>A standard object where the key is the name of the grouping, and the value is a an array of namespaced message bundle keys.
        <pre><code>stringArrayIndex: {
    someGroup: ["myNamespace-string1", "myNamespace-string2"]
}</code></pre></td>
        <td>
        <pre><code>stringArrayIndex: {}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`rendererOptions`</td>
        <td>Only used when combined with a rendererComponent. This option is used to override the default messageLocator used by the renderer.<br/><strong>NOTE</strong>: In general this should not be modified.</td>
        <td></td>
        <td>
        <pre><code>rendererOptions: {
    messageLocator: "{msgResolver}.resolve"
}</code></pre>
        </td>
    </tr>
</table>

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
```

