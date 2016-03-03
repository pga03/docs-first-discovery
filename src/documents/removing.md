---
title: Less simple: Removing preferences
layout: default
category: Tutorials
---

Your flying car doesn’t support some of the preferences in the First Discovery Tool – in particular, "Captions" and "On-Screen Keyboard" preferences. You want to remove those preferences entirely.
## Quick version
1. Edit `firstDiscoveryPrefsServerIntegration.html` to remove the placeholders for the panels.
2. Edit `schemas.js` to remove code for the panels from the auxiliary schema.
3. Edit `src/schemas/schemas.js` to remove code for the preferences from the primary schema.
4. Edit `src/html/confirmTemplate.html` to remove the preferences in the preferences table on the confirm panel. 
5. Edit `src/js/panels.js` (and optionally) `src/messages/confirm_en-US.json` to remove remaining code for the removed preferences. 

## Detailed Instructions

1. Edit `src/html/firstDiscoveryPrefsServerIntegration.html` to remove the placeholders for the panels.

    A. In the `firstDiscoveryPrefsServerIntegration.html` file, find the `<section>` elements for the panels we want to remove. Look for the class names `"gpiic-fd-prefsEditor-panel-captions"` and `"gpiic-fd-prefsEditor-panel-onScreenKeyboard"`.

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

    B. Remove each of the `<section>` elements completely for those classes mentioned above.
    
    Now that the placeholders for these panels are removed, these preferences will no longer appear to the user while going through the tool.

2. Edit `src/schemas/schemas.js` to remove code for the panels from the auxiliary schema.

    The `src/js/schemas.js` contains the primary schema (which defines the preferences) and the auxiliary schema (which defines the editor itself, i.e. the panels used to adjust the preferences, where to find HTML templates, etc).

    A. In the `schemas.js` file, find the auxiliary schema, which starts with `fluid.defaults("gpii.firstDiscovery.auxSchema", `.

    ```javascript
    fluid.defaults("gpii.firstDiscovery.auxSchema", {
        gradeNames: ["fluid.prefs.auxSchema"],
        auxiliarySchema: {
            "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor"],
            // more not shown here
    ```

    B. Inside the section named `"auxiliarySchema"`, find the properties that are named to match the preferences we want to remove. Look for `"captions"` and `"onscreenKeyboard"`.

    ```javascript
    //more content not shown here
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
    //more content not shown here
    },
    ```
    D. Remove the properties for the preferences you wish to remove, including the keys.
    
3. Edit `src/schemas/schemas.js` to remove code for the preferences from the primary schema.

    A. In the `schemas.js` file, find the primary schema. It is a list of `fluid.defaults()` calls for each of the preferences, starting with `"gpii.firstDiscovery.schemas.language"`.
    
    B. Find the `fluid.defaults()` calls for the preferences we want to remove. Look for `"gpii.firstDiscovery.schemas.captions"` and `"gpii.firstDiscovery.schemas.onscreenKeyboard"`.

    ```javascript
    //more content not shown here
    fluid.defaults("gpii.firstDiscovery.schemas.onScreenKeyboard", {
        gradeNames: ["fluid.prefs.schemas"],
        schema: {
            "gpii.firstDiscovery.onScreenKeyboard": {
                "type": "boolean",
                "default": false
            }
        }
    });
    
    fluid.defaults("gpii.firstDiscovery.schemas.captions", {
        gradeNames: ["fluid.prefs.schemas"],
        schema: {
            "gpii.firstDiscovery.captions": {
                "type": "boolean",
                "default": true
            }
        }
    });
    //more content not shown here
    ```
    
    C. Remove the `fluid.defaults()` calls for the preferences you want to remove. 
    
    Now that these preferences are removed rom the primary schema, not only are they not presented to the user, but they are also not saved with the users other preferences with a default value. Since they are removed from the primary schema, these preferences do not exist in the tool at all.
    
    Now that these preferences do not exist, you'll want to have them removed from the preferences table on the confirm panel.
     
4. Edit `src/html/confirmTemplate.html` to remove the preferences in the preferences table on the confirm panel. 

    A. In `confirmTemplate.html`, find the table declaration with the class `"gpii-fd-confirm-table"`, and search for the `<tr>` declarations for the preferences we want to remove.
    
    ```html
    <table class="gpii-fd-confirm-table">
    //more content not shown here
    <tr class="captions">
        <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
        <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span></td>
    </tr>
    <tr class="onScreenKeyboard">
        <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
        <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span></td>
    </tr>
    //more content not shown here
    ```
    
    B. Remove the `<tr>` declarations for the preferences you want to remove. 
    
    Now that the preferences are removed from the preferences table, you'll want to remove the voicing for those preferences as well.
    
    C. Find the `<p>` declarations with the "tts" class declarations for the preferences we want to remove. (`captions-tts` and `onScreenKeyboard-tts`)
    
    ```html
    <p class="gpii-fd-hidden-accessible gpiic-fd-panel-content-tts captions-tts"></p>
    <p class="gpii-fd-hidden-accessible gpiic-fd-panel-content-tts onScreenKeyboard-tts"></p>
    ```
    
    D. Remove those `<p>` declarations. 
    
    Now the preferences have been completely removed from the tool and will no longer appear in the preferences table on the confirm panel, or be voiced on the confirm panel.
    
    We are still not finished though. There is still some remaining code for the preferences that hasn't been removed that, because the preferences no longer exist, can cause some runtime errors. The final step is to do a final sweep of any leftoever code from the preferences we have removed.
    
5. Edit `src/js/panels.js` (and optionally) `src/messages/confirm_en-US.json` to remove remaining code for the removed preferences. 

    A. In  `panels.js`, find the `fluid.defaults()` calls for the preferences we want to remove. The calls are made to `"gpii.firstDiscovery.panel.captions"` and `"gpii.firstDiscovery.panel.onScreenKeyboard"`. Remove these sections of code.
    
    ```javascript
    //more content not shown here
    fluid.defaults("gpii.firstDiscovery.panel.onScreenKeyboard", {
        gradeNames: ["gpii.firstDiscovery.panel.yesNo"],
        preferenceMap: {
            "gpii.firstDiscovery.onScreenKeyboard": {
                "model.value": "default"
            }
        }
    });
    
    fluid.defaults("gpii.firstDiscovery.panel.captions", {
        gradeNames: ["gpii.firstDiscovery.panel.yesNo"],
        preferenceMap: {
            "gpii.firstDiscovery.captions": {
                "model.value": "default"
            }
        }
    });
    //more content not shown here
    ```
    
    Now we need to erase the code that was used to place the preferences on the confirm panel.
    
    B. Find the `fluid.defaults()` call for `"gpii.firstDiscovery.panel.confirm"`.
    
    There are 4 areas we need to remove code for the preferences we are removing from the tool. 1) "Model Relays", 2) "Selectors", 3) "ProtoTree", and 4) "Bindings".
    
    C. Find the `modelRelay: []` section and remove the 2 model relays for each preference you want to remove.  
    
    ```javascript
    //more content not shown here
    {
        source: "{fluid.prefs.prefsEditor}.model.preferences.gpii_firstDiscovery_onScreenKeyboard",
        target: "friendlyNames.onScreenKeyboard",
        singleTransform: {
            type: "fluid.transforms.valueMapper",
            inputPath: "",
            options: {
                true: "{that}.options.messageBase.true",
                false: "{that}.options.messageBase.false"
            }
        }
    },
    {
        source: "friendlyNames.onScreenKeyboard",
        target: "tts.onScreenKeyboard",
        singleTransform: {
            type: "fluid.transforms.stringTemplate",
            template: "%preamble %value %units.",
            terms: {
                preamble: "{that}.options.messageBase.onScreenKeyboardTtsPreamble",
                value: "{that}.model.friendlyNames.onScreenKeyboard",
                units: ""
            }
        }
    },
    //more content not shown here
    {
        source: "{fluid.prefs.prefsEditor}.model.preferences.gpii_firstDiscovery_captions",
        target: "friendlyNames.captions",
        singleTransform: {
            type: "fluid.transforms.valueMapper",
            inputPath: "",
            options: {
                true: "{that}.options.messageBase.true",
                false: "{that}.options.messageBase.false"
            }
        }
    },
    {
        source: "friendlyNames.captions",
        target: "tts.captions",
        singleTransform: {
            type: "fluid.transforms.stringTemplate",
            template: "%preamble %value %units.",
            terms: {
                preamble: "{that}.options.messageBase.captionsTtsPreamble",
                value: "{that}.model.friendlyNames.captions",
                units: ""
            }
        }
    },
    //more content not shown here
    ```
    Each preference has 3 selectors, 1) for the "value", 2) for the "label", and 3) for the "tts".
    
    D. Find the `selectors: {}` section and remove the 3 selectors for each preference you want to remove.  
    
    ```javascript
    selectors: {
        //more content not shown here
        onScreenKeyboardValue: ".onScreenKeyboard .gpii-confirm-value",
        onScreenKeyboardLabel: ".onScreenKeyboard .gpii-confirm-label",
        onScreenKeyboardTts: ".onScreenKeyboard-tts",
        captionsValue: ".captions .gpii-confirm-value",
        captionsLabel: ".captions .gpii-confirm-label",
        captionsTts: ".captions-tts",
        //more content not shown here
    }
    ```
    
    Each preference has 3 protoTree values, 1) for the "value", 2) for the "label", and 3) for the "tts".
    
    E. Find the `protoTree: {}` section and remove the 3 selectors for each preference you want to remove.  
    
    ```javascript
    protoTree: {
        //more content not shown
        onScreenKeyboardLabel: {messagekey: "onScreenKeyboardLabel"},
        onScreenKeyboardValue: {messagekey: "onScreenKeyboardValue"},
        onScreenKeyboardTts: {messagekey: "onScreenKeyboardTtsPreamble"},
        captionsLabel: {messagekey: "captionsLabel"},
        captionsValue: {messagekey: "captionsValue"},
        captionsTts: {messagekey: "captionsTtsPreamble"},
        //more content not shown
    }
    ```
    
    Each preference has 2 protoTree values, 1) for the "value" and 2) for the "tts".
    
    F. Find the `bindings: {}` section and remove the 2 selectors for each preference you want to remove.
      
    ```javascript
    bindings: {
        //more content not shown
        "onScreenKeyboardValue": "friendlyNames.onScreenKeyboard",
        "onScreenKeyboardTts": "tts.onScreenKeyboard",
        "captionsValue": "friendlyNames.captions",
        "captionsTts": "tts.captions",
        //more content not shown
    }
    ```
    
    Now all of the code to place the preference on the confirm panel has been removed.
    
    The last steps are optional because they will not effect the tool, however, removing unused code is good practice.
    
    The `src/messages/confirm_en-US.json` file holds "friendly name" and "tts" values for the preferences we have removed. Since they are no longer used, we should remove them. 
    
    For each preference, there are 2 friendly name values, 1) for the "label", and 2) for the "value", as well as 3) a "tts preamble".
    
    G. (optional) In `confirm_en-US.json`, remove the 3 values for the preferences we want to remove. 
    
    ```javascript
    {
        //more content not shown
        "onScreenKeyboardLabel": "On-Screen Keyboard:",
        "onScreenKeyboardValue": "",
        "captionsLabel": "Captions:",
        "captionsValue": "",
        //more content not shown
        "onScreenKeyboardTtsPreamble": "Your on screen keyboard choice is",
        "captionsTtsPreamble": "Your captions choice is",
        //more content not shown
    }
    ```
    
    H. (optional) repeat step "G" for the alternate language files, for example, `src/messages/confirm_fr-FR.json`.
    
    The last step is to delete the message files used on the preference panel. For each preference there is a `en-US` for English, `fr-FR` for French, and `es-MX` for Spanish (these are currently the only three supported languages in the tool).
    
    I. (optional) Delete the `en-US`, `fr-FR`, and `es-MX` message files for each preference (as well as any other language versions for that preference). For example, `captions_en-US.json`, `captions_fr-FR.json`, and `captions_es-MX.json`.