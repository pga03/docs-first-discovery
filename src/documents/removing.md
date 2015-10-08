---
title: Less simple: Removing preferences
layout: default
category: Tutorials
---

Your flying car doesn’t support some of the preferences in the First Discovery Tool – in particular, contrast, captions and keyboard preferences. You want to remove those preferences entirely.
## Quick version
1. Edit `demos/index.html` to remove the icons at the bottom of the screen.
2. Edit `firstDiscovery.html` to remove the placeholders for the panels.
3. Edit `schemas.js` to remove code for the panels from the auxiliary schema.

## Detailed Instructions

1. Edit `demos/index.html` to remove the icons at the bottom of the screen.

    A. In the `demos/index.html` file, find the list of icons (a `<ul>` with the class `"gpii-fd-navIcon-outer"`  as described above).

    B. Find the `<li>` elements for the preferences we want to remove. Look for the class names `"gpii-fd-contrast"`, `"gpii-fd-captions"` and `"gpii-fd-prefsEditor-panel-onScreenKeyboard"`.

    ```html
    <ul class="gpii-fd-navIcon-outer">
        <!-- some list items not shown -->
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-speechRate">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-contrast">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-text">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-onScreenKeyboard">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-captions">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-keyboard">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <!-- some list items not shown -->
    </ul>
    ```

    C. Remove the `<li>` elements, with all of their contents.

2. Edit `src/html/firstDiscovery.html` to remove the placeholders for the panels.

    A. In the `src/html/firstDiscovery.html` file, find the `<section>` elements for the panels we want to remove. Look for the class names `"gpiic-fd-prefsEditor-panel-contrast"`, `"gpiic-fd-prefsEditor-panel-captions"` and `"gpiic-fd-prefsEditor-panel-onScreenKeyboard"`.

    ```html
    <section class="gpiic-fd-prefsEditor-panel-lang gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-lang gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-welcome gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-welcome gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-showSounds gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-showSounds gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speakText gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speakText gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speechRate gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speechRate gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-contrast gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-contrast gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-size gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-size gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-onScreenKeyboard gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-onScreenKeyboard gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-captions gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-captions gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-keyboard gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-keyboard gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-congratulations gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-congratulations gpii-fd-main"></section>
    ```

    B. Remove the `<section>` elements completely.

3. Edit `src/js/schemas.js` to remove code for the panels from the auxiliary schema.

    A. The `src/js/schemas.js` contains the primary schema (which defines the preferences) and the auxiliary schema (which defines the editor itself, i.e. the panels used to adjust the preferences, where to find HTML templates, etc).

    You can see the entire file here: https://github.com/fluid-project/first-discovery/blob/master/src/js/schemas.js

    B. In the `schemas.js` file, find the auxiliary schema, which starts with `fluid.defaults("gpii.firstDiscovery.auxSchema", `.

    ```javascript
    fluid.defaults("gpii.firstDiscovery.auxSchema", {
        gradeNames: ["fluid.prefs.auxSchema"],
        auxiliarySchema: {
            "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor"],
            // more not shown here
    ```

    C. Inside the section named `"auxiliarySchema"`, find the properties that are named to match the preferences we want to remove. Look for `"contrast"`, `"captions"` and `"onscreenKeyboard"`.

    ```javascript
    "speechRate": {
        "type": "gpii.firstDiscovery.speechRate",
        "panel": {
            "type": "gpii.firstDiscovery.panel.speechRate",
            "container": ".gpiic-fd-prefsEditor-panel-speechRate",
            "template": "%templatePrefix/rangeWithDisabledMsgTemplate.html",
            "message": "%messagePrefix/speechRate.json",
            "gradeNames": ["gpii.firstDiscovery.panel.speechRate.prefsEditorConnection"]
        }
    },
    "contrast": {
        "type": "fluid.prefs.contrast",
        "classes": {
            "default": "fl-theme-prefsEditor-default",
            "bw": "fl-theme-prefsEditor-bw fl-theme-bw",
            "wb": "fl-theme-prefsEditor-wb fl-theme-wb"
        },
        "enactor": {
            "type": "fluid.prefs.enactor.contrast",
            "classes": "@contrast.classes"
        },
        "panel": {
            "type": "gpii.firstDiscovery.panel.contrast",
            "container": ".gpiic-fd-prefsEditor-panel-contrast",
            "classnameMap": {"theme": "@contrast.classes"},
            "template": "%templatePrefix/contrast.html",
            "message": "%messagePrefix/contrast.json"
        }
    },
    "textSize": {
        "type": "fluid.prefs.textSize",
        "enactor": {
            "type": "fluid.prefs.enactor.textSize"
        },
        "panel": {
            "type": "gpii.firstDiscovery.panel.textSize",
            "container": ".gpiic-fd-prefsEditor-panel-size",
            "template": "%templatePrefix/rangeTemplate.html",
            "message": "%messagePrefix/textSize.json"
        }
    },
    "onScreenKeyboard": {
        "type": "gpii.firstDiscovery.onScreenKeyboard",
        "panel": {
            "type": "gpii.firstDiscovery.panel.onScreenKeyboard",
            "container": ".gpiic-fd-prefsEditor-panel-onScreenKeyboard",
            "template": "%templatePrefix/yesNo.html",
            "message": "%messagePrefix/onScreenKeyboard.json"
        }
    },
    "captions": {
        "type": "gpii.firstDiscovery.captions",
        "panel": {
            "type": "gpii.firstDiscovery.panel.captions",
            "container": ".gpiic-fd-prefsEditor-panel-captions",
            "template": "%templatePrefix/yesNo.html",
            "message": "%messagePrefix/captions.json"
        }
    },
    "showSounds": {
        "type": "gpii.firstDiscovery.showSounds",
        "panel": {
            "type": "gpii.firstDiscovery.panel.showSounds",
            "container": ".gpiic-fd-prefsEditor-panel-showSounds",
            "template": "%templatePrefix/yesNo.html",
            "message": "%messagePrefix/showSounds.json"
        }
    },
    ```
    D. Remove the properties, including the keys.

