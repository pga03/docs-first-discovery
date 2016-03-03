---
title: More complicated: Adding a simple preference
layout: default
category: Tutorials
---

Your flying car has an "Autopilot" feature, and you want to add a preference for this. It’s a boolean preference, i.e. "Do you want autopilot turned on by default?" with a simple yes or no answer. After creating this new preference, and adding a new panel for the "Autopilot" preference, you will need to add the preference and its value to the preferences table on the confirm panel.

## Quick version

1. Edit `src/schemas/schemas.js` to add the "Autopilot" preference to the primary schemas.
2. Create JSON files in the messages folder with the necessary strings.
3. Edit `src/html/firstDiscoveryPreferencesServerIntegration.html` to add a placeholder for the panel.
4. Edit `src/js/panels.js` to add the code that creates the panel for the "Autopilot" preference.
5. Edit `src/schemas/schemas.js` to add code for the panel to auxiliary schema.
6. Edit `src/messages/confirm_en-US.json` to add the `"friendlyNames"` and `"tts"` values for the confirm panel.
7. Edit `src/js/panels.js` to add the "model relays" for the "Autopilot" preference.
8. Edit `src/js/panels.js` to add the "selectors" for the "Autopilot" preference.
9. Edit `src/js/panels.js` to add the "protoTree" options for the "Autopilot" preference.
10. Edit `src/js/panels.js` to add the "bindings" for the "Autopilot" preference.
11. Edit `src/html/confirmTemplate.html` to add the preference to the preferences table on the confirm panel.
12. Edit `src/html/confirmTemplate.html` to add the preference to be read by "tts".


## Detailed Instructions

1. Edit `src/schemas/schemas.js` to add the "Autopilot" preference to the primary schemas.

    A. The `src/schemas/schemas.js` file contains the primary schema, which defines the preferences, and the auxiliary schema, which defines the editor itself (i.e. the panels used to adjust the preferences, where to find HTML templates, etc.)

    You can see the entire file here: https://github.com/GPII/first-discovery/blob/master/src/schemas/schemas.js

    B. In the `schemas.js` file, find the definition of the "speak" primary schema, which starts with `fluid.defaults("gpii.firstDiscovery.schemas.speak", `:

    ```javascript
    fluid.defaults("gpii.firstDiscovery.schemas.speak", {
        gradeNames: ["fluid.prefs.schemas"],
            schema: {
              "gpii.firstDiscovery.speak": {
                   "type": "boolean",
                    "default": true
                }
            }
    });
    ```

    This preference is a boolean preference, and follows the "yesNo" preference template, just like the "Autopilot" preference we want to add.

    C. Add a new definition that takes the same form as the "speak" preference, but with "autopilot" instead of "speak". Change the default value to false (since we probably don’t want the car to just start out with auto-pilot on):

    ```javascript
    fluid.defaults("gpii.firstDiscovery.schemas.autopilot", {
        gradeNames: ["fluid.prefs.schemas"],
            schema: {
              "gpii.firstDiscovery.autopilot": {
                   "type": "boolean",
                    "default": false
                }
            }
    });
    ```

2. Create JSON files in the src/messages folder with the necessary strings for the panel.

    A. The src/messages folder contains JSON files containing the interface strings for each preference panel. The file `"speakText_en-US.json"` is an example of the form of message file you’ll create for your preference panel.

    You can see that file here: https://github.com/GPII/first-discovery/blob/master/src/messages/speakText_en-US.json

    B. Create a new file in the messages folder called `"autopilot_en-US.json"`.

    C. Edit the contents of the file according to the Autopilot functionality:
    * Define the "instructions" as "Do you want autopilot turned on?";
    * Define the "yes-tooltip" as "Select to turn autopilot on";
    * Define the "no-tooltips"Select to turn autopilot off";
    * Define the "yes-tooltipAtSelect" as "Autopilot is on";
    * Define the "no-tooltipAtSelect" as "Autopilot is off".

    ```javascript
    {
        "instructions": "Do you want autopilot turned on?",
        "no": "No",
        "yes": "Yes",

        "yes-tooltip": "Select to turn autopilot on",
        "no-tooltip": "Select to turn autopilot off",
        "yes-tooltipAtSelect": "Autopilot is on",
        "no-tooltipAtSelect": "Autopilot is off"
    }
    ```

    D. Duplicate the file for other languages; for example, create a file called `"autopilot_fr-FR.json"` for a French version. Use exactly the same keys in the file, but change the values to the translated strings:

    ```javascript
    {
        "instructions": "Voulez-vous le pilote automatique activé par défaut??",
        "no": "Non",
        "yes": "Oui",

        "yes-tooltip": "Sélectionner pour activer le pilote automatique",
        "no-tooltip": "Sélectionner pour désactiver le pilote automatique",
        "yes-tooltipAtSelect": "Pilote automatique est activée",
        "no-tooltipAtSelect": "Pilote automatique est désactivée"
    }
    ```
	(The currently supported languages in the tool are en-US English, fr-FR French, and es-MX Spanish; The remaining language options in the tool are not suported and do not require message files; Unsupported languages defualt to English)

3. Edit `src/html/firstDiscoveryPreferenceServerIntegration.html` to add a placeholder for the panel.

    A. Add a new `<section>` element of the same form as the others, but define the class names to reflect the "Autopilot" preference:

    ```html
    <section class="gpiic-fd-prefsEditor-panel-lang gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-lang gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-welcome gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-welcome gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-showSounds gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-showSounds gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-autopilot gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-autopilot gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speakText gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speakText gpii-fd-main"></section>   
     
    //more content not shown
    ```

    Make sure that the new `<section>` element places the panel in the order that you want the preferences. You can see the new `<section>` for `"gpiic-fd-prefsEditor-panel-autopilot"` is placed between the `"showSounds"` and `"speakText"` sections. Be sure to use this same position for other added elements for the "Autopilot" preference.
    
4. Edit `src/js/panels.js` to add the code that creates the panel for the "Autopilot" preference.

    A. In `panels.js`, make a call to `fluid.defualts()` to create the the panel, and call `"gpii.firstDiscovery.panel.autopilot"`: 

    ```javascript
        fluid.defaults("gpii.firstDiscovery.panel.autopilot", {
            // configuration options will go here
        });
    ```

    `fluid.defaults()` is one of the core functions in Infusion: It is used to create components (the building blocks of any Infusion application) and register them with the Framework.

    E. Fill in the configuration options for the panel:

    The First Discovery Tool currently presents four basic ‘styles’ of preference: 1) basic yes/no questions, 2) a range of values (like the text size), 3) a set of choices (like the colour combinations), and 4) the keyboard adjustments.

    The code for the First Discovery Tool includes some base grades that can be used to implement a panel of one of these types (including the HTML template, and the CSS for styling). These base grades define most of the functionality for a particular type of panel; using these grades will effectively ‘inherit’ this functionality.

    For a boolean preference, the First Discovery Tool has a grade called `"gpii.firstDiscovery.panel.yesNo"` that provides most of the functionality for a simple yes/no panel:

    ```javascript
        fluid.defaults("gpii.firstDiscovery.panel.autopilot", {
            gradeNames: ["gpii.firstDiscovery.panel.yesNo"],
            // more options will go here
        });
    ```

    (You will see in the code that other panel types have different grades specified in the gradeNames option.)
    Every panel needs a preferenceMap option to tell the framework how to map the preference in the Primary Schema to the panel:

    ```javascript
        fluid.defaults("gpii.firstDiscovery.panel.autopilot", {
            gradeNames: ["gpii.firstDiscovery.panel.yesNo"],
            preferenceMap: {
                "gpii.firstDiscovery.autopilot": {
                    "model.value": "default"
                }
            }
        });
    ```

5. Edit `src/schemas/schemas.js` to add code for the panel to the auxiliary schema.

    The `src/schemas/schemas.js` file contains the auxiliary schema, which defines the editor itself (i.e. the panels used to adjust the preferences, where to find HTML templates, etc.)

    A. In the `schemas.js` file, find the auxiliary schema, which starts with `fluid.defaults("gpii.firstDiscovery.auxSchema", `.

    ```javascript
    fluid.defaults("gpii.firstDiscovery.auxSchema", {
        gradeNames: ["fluid.prefs.auxSchema"],
        auxiliarySchema: {
            "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor"],
            // more not shown here
    ```

    B. Inside the section named "auxiliarySchema", add a section for the new panel. You can see that here we specify the "yesNo" format as the template, by using  `%templatePrefix/yesNo.html`, and the message file for the text on screen is linked under the message option with the value `%messagePrefix/autopilot.json`.

    ```javascript
    fluid.defaults("gpii.firstDiscovery.auxSchema", {
        gradeNames: ["fluid.prefs.auxSchema"],
        auxiliarySchema: {
            "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor"],
            "namespace": "gpii.firstDiscovery",
            "terms": {
                "templatePrefix": "../src/html",
                "messagePrefix": "../src/messages"
            },
            "template": "%templatePrefix/firstDiscovery.html",
            "message": "%messagePrefix/firstDiscovery.json",
            "lang": {
                // some content not shown
            },
            "welcome": {
                // some content not shown
            },
            "speakText": {
                // some content not shown
            },
            "autopilot": {
                "type": "gpii.firstDiscovery.autopilot",
                "panel": {
                    "type": "gpii.firstDiscovery.panel.autopilot",
                    "container": ".gpiic-fd-prefsEditor-panel-autopilot",
                    "template": "%templatePrefix/yesNo.html",
                    "message": "%messagePrefix/autopilot.json"
                }
            },
            // more content not shown
        }
    });
    ```
    
    At this point, you should have a new panel in the tool with a new preference called "Autopilot" that follows the "yesNo" template, and uses the text you specified in the message files. This panel should be able to self voice the instructions, buttons, and tooltips. Changing the language setting should use the alternate the text in the panel with the corresponding language selection. 	

    Now that you have a working panel and preference, you'll want to have that preference appear in on the confirm page so that the user can make sure that your new preference is set how they want it.

6. Edit `src/messages/confirm_en-US.json` to add the `"friendlyNames"` and `"tts"` values for the confirm panel.

    Each preference is relayed from the "prefsEditor" and transformed into a user friendly name, or `"friendlyName"`, which is defined here. Example: "en-US" becomes "English". The table needs a friendly name value for the preference "label", which goes in the left column of the table, and a "value", in the right column.  
    
    A. Add the `"friendlyNames"` "label" and "value" for the "Autopilot" preference in the `confirm_en-US.json` message file. 
    
    ```javascript
    "autopilotLabel": "Autopilot:",
    "autopilotValue": ""
    ```
    
    Note: the "value" friendly name is left blank here. That's because we will retrieve the value and insert it there later in the code.
    
    Each friendly name preference from this model is relayed to `"tts"` and merged into the string template with its preamble, value, and (occasionally) units. The tts values are used for text to speech to voice the contents of the confirmation panel. Example: "English" -> "Your language choice is English". Example: "true" -> "Your use captions choice is ON".
    
    B. Add the "tts" preamble for the "Autopilot" preference.
    
    ```javascript
    "autopilotLabel": "Autopilot:",
    "autopilotValue": "",
    "autopilotTtsPreamble": "Your autopilot choice is"
    ```
    
    C. Repeat step 6 for all other supported languages. 
    
    For example, open `src/messages/confirm_fr-FR.json`, and add the following for French translations. 
    
    ```javascript
    "autopilotLabel": "Pilote Automatique:",
    "autopilotValue": "",
    "autopilotTtsPreamble": "Votre choix est le pilote automatique"
    ```
     
7. Edit `src/js/panels.js` to add the "model relays" for the "Autopilot" preference.

    A. Navigate to the `"fluid.defaults()"` call to `"gpii.firstDiscovery.panel.confirm"`, and find the section for `""modelRelay[]`.
 
    This panel uses many modelRelays. The modelRelays populate two model values in this panel,`"friendlyNames"` and `"tts"`, which were defined in the previous step.
    
    Take, for example, the model relays for the "Speak" preference, another simple preference that follows the "yesNo" template. 
    
    ```javascript
    //more content not shown here
    {
        source: "{fluid.prefs.prefsEditor}.model.preferences.gpii_firstDiscovery_speak",
        target: "friendlyNames.speak",
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
        source: "friendlyNames.speak",
        target: "tts.speak",
        singleTransform: {
            type: "fluid.transforms.stringTemplate",
            template: "%preamble %value %units.",
            terms: {
                preamble: "{that}.options.messageBase.speakTtsPreamble",
                value: "{that}.model.friendlyNames.speak",
                units: ""
            }
        }
    },
    //more content not shown here
    ```
    
    B. Using the "Speak" preference template above, add the model relays for the "Autopilot" preference in the `"modelRelay: []"` section.
    
    ```javascript
    //more content not shown here
    {
        source: "{fluid.prefs.prefsEditor}.model.preferences.gpii_firstDiscovery_autopilot",
        target: "friendlyNames.autopilot",
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
        source: "friendlyNames.autopilot",
        target: "tts.autopilot",
        singleTransform: {
            type: "fluid.transforms.stringTemplate",
            template: "%preamble %value %units.",
            terms: {
                preamble: "{that}.options.messageBase.autopilotTtsPreamble",
                value: "{that}.model.friendlyNames.autopilot",
                units: ""
            }
        }
    },
    //more content not shown here
    ```
    
8. Edit `src/js/panels.js` to add the "selectors" for the "Autopilot" preference.

    A. In `"gpii.firstDiscovery.panel.confirm"`, find the `selectors: {}` section. 
    
    Each preference requires 3 different "selectors", 1) a "value" selector, 2) a "label" selector, and 3) a "tts" selector. Take, for example, the selectors for the "Speak" preference.
    
    ```javascript
    speakValue: ".speak .gpii-confirm-value",
    speakLabel: ".speak .gpii-confirm-label",
    speakTts: ".speak-tts"
    ```
    
    B. Add the selectors for the "Autopilot" preference, following the template of the "Speak" preference.
    
    ```javascript
    autopilotValue: ".autopilot .gpii-confirm-value",
    autopilotLabel: ".autopilot .gpii-confirm-label",
    autopilotTts: ".autopilot-tts"
    ```
    
9. Edit `src/js/panels.js` to add the "protoTree" options for the "Autopilot" preference.

    A. In `"gpii.firstDiscovery.panel.confirm"`, find the `protoTree: {}` section. 
    
    The "ProtoTree" helps with the rendering of the panel. This is where we tell the renderer what to place on the screen.
    
    Similar to "selectors", each preference also requires 3 different "protoTree" options, 1) "value", 2) "label" , and 3) "tts". Take, for example, the protoTree options for the "Speak" preference.
    
    ```javascript
    speakLabel: {messagekey: "speakLabel"},
    speakValue: {messagekey: "speakValue"},
    speakTts: {messagekey: "speakTtsPreamble"}
    ```
    
    B. Add the "protoTree" options for the "Autopilot" preference, following the template of the "Speak" preference. 
    
    ```javascript
    autopilotLabel: {messagekey: "autopilotLabel"},
    autopilotValue: {messagekey: "autopilotValue"},
    autopilotTts: {messagekey: "autopilotTtsPreamble"}
    ```
    
10. Edit `src/js/panels.js` to add the "bindings" for the "Autopilot" preference.

    A. In `"gpii.firstDiscovery.panel.confirm"`, find the `bindings: {}` section. 
    
    These "bindings" variables compose the "value" and "tts" strings that wil be used on the confirmation panel. Take, for example, the "bindings" for the "Speak" preference.
    
    ```javascript
    "speakValue": "friendlyNames.speak",
    "speakTts": "tts.speak"
    ```
    
    B. Add the "bindings" options for the "Autopilot" preference, following the template of the "Speak" preference.
    
    ```javascript
    "autopilotValue": "friendlyNames.autopilot",
    "autopilotTts": "tts.autopilot"
    ```
    
11. Edit `src/html/confirmTemplate.html` to add the preference to the preferences table on the confirm panel.

    A. Navigate to the preferences table declaration, with the class `"gpii-fd-confirm-table"`.
    
    Here you can see each preference has its own `<tr>` declaration, with 2 `<td>` declarations in each, 1) for the preference label, and 2) for the preference value. Take, for example, the "Speak" preference `<tr>` section. 
    
    ```html
    <table class="gpii-fd-confirm-table">
        //more content not shown here
        <tr class="speak">
            <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
            <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span></td>
        </tr>
        //more content not shown here
    </table>
    ```
    
    B. In the correct order of preferences (between "showSounds" and "speakText"), add a new `<tr>` declaration with the class `"autopilot"`.
    
    ```html
        <table class="gpii-fd-confirm-table">
            //more content not shown here
            
            <tr class="showSounds">
                <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
                <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span></td>
            </tr>
            <tr class="autopilot">
                <td></td>
                <td></td>
            </tr>  
            <tr class="speak">
                <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
                <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span>
                </td>
            </tr>
            //more content not shown here
        </table>
    ```
    
    C. Add the class for the label `<td>` of "autopilot" with `"gpii-fd-confirm-table-name"`, and Inside it add a `<span>` with the class `"gpii-confirm-label "`.
    
    ```html
    <tr class="autopilot">
        <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
        <td></td>
    </tr>  
    ```
    
    D. Add the class for the value `<td>` of "autopilot" with `"gpii-fd-confirm-table-value"`, a `<span>` with the class `"gpii-confirm-value "`, and a second `<span>` with the class `"gpii-confirm-unit "`.
    
    ```html
    <tr class="autopilot">
        <td class="gpii-fd-confirm-table-name"><span class="gpii-confirm-label "></span></td>
        <td class="gpii-fd-confirm-table-value"><span class="gpii-confirm-value "></span><span class="gpii-confirm-unit "></span>
    </tr>  
    ```
    
12. Edit `src/html/confirmTemplate.html` to add the preference to be read by "tts".

    A. In the confirm template, find the section of `<p>` declarations all with the class `gpii-fd-hidden-accessible`.
    
    These `<p>` declarations place the "tts" preferences strings on the panel so that they can be read allowed, but are given the CSS class `gpii-fd-hidden-accessible` so that they do not appear to the user. Take, for example, the `<p>` declaration for the "Speak" preference.
    
    ```html
    <p class="gpii-fd-hidden-accessible gpiic-fd-panel-content-tts speak-tts"></p>
    ```
    
    B. In the correct order of preferences (between "showSounds" and "speakText"), add a new `<p>` declaration with the classes `"autopilot"`.

    ```html
    <p class="gpii-fd-hidden-accessible gpiic-fd-panel-content-tts autopilot-tts"></p>
    ```
    
    After completion of this step, you should have a new preference called "Autopilot" on a new panel, with its name and value in the preferences table on the confirm panel. The voicing for the table should include the "Autopilot" preference and correct value. The text and TTS for the preference should update with the language. 