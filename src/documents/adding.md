---
title: More complicated: Adding a simple preference
layout: default
category: Tutorials
---

Your flying car has an "Autopilot" feature, and you want to add a preference for this. It’s a boolean preference, i.e. "Do you want autopilot turned on by default?" with a simple yes or no answer. After creating this new preference, and adding a new panel for the "Autopilot" preference, you will need to add the preference and its value to the preferences table on the confirm panel.

## Quick version

1. Edit `src/schemas/schemas.js` to add the "Autopilot" preference to the primary schemas.
2. Create JSON files in the messages folder with the necessary strings.
3. Edit `src/html/firstDiscoveryPreferenceServerIntegration.html` to add a placeholder for the panel.
4. Edit `src/js/panels.js` to add the code that creates the panel for the "Autopilot" preference.
5. Edit `src/schemas/schemas.js` to add code for the panel to auxiliary schema.
6. Edit `src/js/panels.js` to add the selectors for the "Autopilot" preference.  
7. Edit `src/js/panels.js` to add Friendly Names for the preference.
8. Edit `src/js/panels.js` to assign the selectors equal to the friendly names. 
9. Edit `src/html/confirmTemplate.html` to add the space for the "Autopilot" preference in the preferences table on the confirm panel.

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

    A. The `src/schemas/schemas.js` file contains the auxiliary schema, which defines the editor itself (i.e. the panels used to adjust the preferences, where to find HTML templates, etc.)

    You can see the entire file here: https://github.com/GPII/first-discovery/blob/master/src/schemas/schemas.js

    B. In the `schemas.js` file, find the auxiliary schema, which starts with `fluid.defaults("gpii.firstDiscovery.auxSchema", `.

    ```javascript
    fluid.defaults("gpii.firstDiscovery.auxSchema", {
        gradeNames: ["fluid.prefs.auxSchema"],
        auxiliarySchema: {
            "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor"],
            // more not shown here
    ```

    C. Inside the section named "auxiliarySchema", add a section for the new panel. You can see that here we specify the "yesNo" format as the template, by using  `%templatePrefix/yesNo.html`, and the message file for the text on screen is linked under the message option with the value `%messagePrefix/autopilot.json`.

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
    
    At this point, you should have a new panel in the tool with a new preference called "Autopilot" that follows the "yesNo" template, and uses the text you specified in the message files. Changing the language setting should use the alternate the text in the panel with the corresponding language selection. 	

    Now that you have a working panel and preference, you'll want to have that preference appear in on the confirm page so that the user can make sure that your new preference is set how they want it.
     
6. Edit `src/js.panels.js` to add the selectors for the "Autopilot" preference. 

    A. Find the `"fluid.defaults()"` call for the confirm panel, which calls `"gpii.firstDiscovery.panel.confirm"`.
    
    B. In the "selectors" option, you will need to add a preference value and preference label for "Autopilot".
    
    ```javascript
    fluid.defaults("gpii.firstDiscovery.panel.confirm", {
            gradeNames: ["fluid.prefs.panel"],
            preferenceMap: {
                "gpii.firstDiscovery.confirm": {}
            },
            selectors: {
                message: ".gpiic-fd-confirm-message",
    
                language: "languageConfirmation",
                languageLabel: "languageLabel",
    
                speak: "speakConfirmation",
                speakLabel: "speakLabel",
                
                autopilot: "autopilotConfirmation",
                autopilotlabel: "autopilotLabel",
    
                speechRate: "speechRateConfirmation",
                speechRateLabel: "speechRateLabel",
                
                //more content not shown
            },
            //more content not shown
    }
    ```
    
7. Edit `src/js.panels.js` to add Friendly Names for the preference. 

    A. In the `"fluid.defaults()"` call to `"gpii.firstDiscovery.panel.confirm"`, find the "friendlyNames" option.
    
    B. For each language, you will need to add a new label in the "labels" section for the "Autopilot" preference that follows the same format as the other preferences' friendly names. For unsupported languages, use the English value for the preference. 
    
    ```javascript
    fluid.defaults("gpii.firstDiscovery.panel.confirm", {
            gradeNames: ["fluid.prefs.panel"],
            preferenceMap: {
                "gpii.firstDiscovery.confirm": {}
            },
            
            //more content not show here
            
            friendlyNames: {
                            "en-US": {
                                labels: {
                                    language: "Language:",
                                    speak: "Text to Speech:",
                                    autopilot: "Autopilot:",
                                    speechRate: "Speech Rate:",
                                    contrast: "Contrast:",
                                    textSize: "Text Size:",
                                    letterSpace: "Letter Spacing:",
                                    lineSpace: "Line Spacing:",
                                    onScreenKeyboard: "On-Screen Keyboard:",
                                    captions: "Captions:",
                                    showSounds: "Show Sounds:",
                                    stickyKeys: "Sticky Keys:"
                                },
                                //more content not shown here
                                }
                            },
                            "fr-FR": {
                                labels: {
                                    language: "Langue:",
                                    speak: "Synthèse Vocale:",
                                    autopilot: "Pilote Automatique:",
                                    speechRate: "Débit de Parole:",
                                    contrast: "Contraste:",
                                    textSize: "Taille du Texte:",
                                    letterSpace: "L'espacement des Lettres",
                                    lineSpace: "Interligne:",
                                    onScreenKeyboard: "Clavier à l'Écran:",
                                    captions: "Légendes:",
                                    showSounds: "Voir les Sons:",
                                    stickyKeys: "Touches Rémanentes:"
                                },
                                //more content not shown here
                                }
                            },
                            
                            //more content not shown here
            }
    });
    ```
    
    Since the "Autopilot" preference follows the "yesNo" template, it will use the "onOff" friendly name "values". If your new preference used other values, you would need to create those friendly names in the "values" section of "friendlyNames".
    
    C. (Optional) For each language, create a new section under the "values" section for the "Autopilot" preference with the possible values and corresponding friendly names.
    
    ```javascript
    fluid.defaults("gpii.firstDiscovery.panel.confirm", {
                gradeNames: ["fluid.prefs.panel"],
                preferenceMap: {
                    "gpii.firstDiscovery.confirm": {}
                },
                
                //more content not show here
                
                friendlyNames: {
                                "en-US": {
                                    labels: {
                                        //more content not shown here
                                    },
                                    values: {
                                        onOff: {
                                            "true": "On",
                                            "false": "Off"
                                        },
                                        language: "English",
                                        contrast:{
                                            "default": "Original",
                                            "bw": "Black/White",
                                            "wb": "White/Black"
                                        },
                                        autopilot:{
                                            "value1": "Value 1",
                                            "value2": "Value 2",
                                            "value3": "Value 3"
                                        }
                                    }
                                },
                                "fr-FR": {
                                    labels: {
                                        //more content not shown here
                                    },
                                    values: {
                                        onOff: {
                                            "true": "Oui",
                                            "false": "Non"
                                        },
                                        language: "Français",
                                        contrast: {
                                            "default": "Original",
                                            "bw": "Noir/Blanc",
                                            "wb": "Blanc/Noir"
                                        },
                                        autopilot:{
                                            "value1": "Valeur 1",
                                            "value2": "Valeur 2",
                                            "value3": "Valeur 3"
                                        }
                                    }
                                },
                                
                                //more content not shown here
                }
    });
    ```

8. Edit `src/js.panels.js` to assign the selectors equal to the friendly names.

    A. In the `"fluid.defaults()"` call to `"gpii.firstDiscovery.panel.confirm"`, find the `"updatePreferenceValues()"` function.
    
    B. Inside the `"updatePreferenceValues()"` function, following the pattern of the other preferences, add the code to change the "Autopilot" label selector, `"autopilotLabel"`, to use the friendly name assigned in the previous step. 
    
    ```javascript
    gpii.firstDiscovery.panel.confirm.updatePreferenceValues = function(that, changeContext) {
    
            //more content not shown here
            
            var language = changeContext.value.gpii_firstDiscovery_language;
    
            //Language
            $("#" + that.options.selectors.languageLabel).text(that.options.friendlyNames[language].labels.language);
            var languageValue = that.options.friendlyNames[language].values.language;
            $("#" + that.options.selectors.language).text(languageValue);
    
            //Text to Speech
            $("#" + that.options.selectors.speakLabel).text(that.options.friendlyNames[language].labels.speak);
            var speakValue = changeContext.value.gpii_firstDiscovery_speak;
            speakValue = that.options.friendlyNames[language].values.onOff[speakValue];
            $("#" + that.options.selectors.speak).text(speakValue);
    
            //Autopilot
            $("#" + that.options.selectors.autopilotLabel).text(that.options.friendlyNames[language].labels.autopilot);
               
            //more content not shown here
    };
    ```
    
    C. Add the code for the "Autopilot" preference to retrieve the value of "Autopilot" and set it equal to a new variable `"autopilotValue"`.
    
    ```javascript
    gpii.firstDiscovery.panel.confirm.updatePreferenceValues = function(that, changeContext) {
        
            //more content not shown here
        
            //Autopilot
            $("#" + that.options.selectors.autopilotLabel).text(that.options.friendlyNames[language].labels.autopilot);
            var autopilotValue = (changeContext.value.gpii_firstDiscovery_autopilot);
                
            //more content not shown here
    };
    ```
    
    D. Now, use the value of `"autopilotValue"` to find the corresponding friendly name,and set `"autopilotValue"` equal to the new friendly name value. 
    
    ```javascript
    gpii.firstDiscovery.panel.confirm.updatePreferenceValues = function(that, changeContext) {
            
            //more content not shown here
            
            //Autopilot
            $("#" + that.options.selectors.autopilotLabel).text(that.options.friendlyNames[language].labels.autopilot);
            var autopilotValue = (changeContext.value.gpii_firstDiscovery_autopilot);
            autopilotValue = that.options.friendlyNames[language].values.onOff[autopilotValue];
                    
            //more content not shown here
    };
    ```
    
    E. Finally, assign the "Autopilot" value selector, `"autopilot"`, equal to `"autopilotValue"`.
    
    ```javascript
    gpii.firstDiscovery.panel.confirm.updatePreferenceValues = function(that, changeContext) {
                
            //more content not shown here
                
            //Autopilot
            $("#" + that.options.selectors.autopilotLabel).text(that.options.friendlyNames[language].labels.autopilot);
            var autopilotValue = (changeContext.value.gpii_firstDiscovery_autopilot);
            autopilotValue = that.options.friendlyNames[language].values.onOff[autopilotValue];
            $("#" + that.options.selectors.autopilot).text(autopilotValue);
                        
            //more content not shown here
    };
    ```
    
    Now that the preference has been added to the `"updatePreferenceValues()"` function, and the selectors have been assigned, the last step is to take the selectors and place them on the confirm panel in the preferences table. 
    
9. Edit `src/html/confirmTemplate.html` to add the space for the "Autopilot" preference in the preferences table on the confirm panel.

    A. Find the preferences table declaration by the "class" `"gpii-fd-confirm-table"`, and, in the correct order of preferences, add a new row with two placeholders for the preference label and value.
    
    ```html
    <table class="gpii-fd-confirm-table">
        <tr>
            <td class="gpii-fd-confirm-table-name"><span id="languageLabel"></span></td>
            <td class="gpii-fd-confirm-table-value"><span id="languageConfirmation"></span></td>
        </tr>
        <tr>
            <td class="gpii-fd-confirm-table-name"><span id="speakLabel"></span></td>
            <td class="gpii-fd-confirm-table-value"><span id="speakConfirmation"></span></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td class="gpii-fd-confirm-table-name"><span id="speechRateLabel"></span></td>
            <td class="gpii-fd-confirm-table-value"><span id="speechRateConfirmation"></span></td>
        </tr>
        
        //more content not shown here
        
    </table>
    ```
    
    B. Add the "Autopilot" preference label to the table, with a "class" of  `"gpii-fd-confirm-table-name"`, and a span with the "id" of `"autopilotLabel"`.
    
    ```html
    <table class="gpii-fd-confirm-table">
       
        //more content not shown here
        
        <tr>
            td class="gpii-fd-confirm-table-name"><span id="newPreferenceLabel"></span></td>
            <td></td>
        </tr>
                   
        //more content not shown here
            
    </table>
    ```
    
    C. Add the "Autopilot" preference value to the table, with a "class" of  `"gpii-fd-confirm-table-value"`, and a span with the "id" of `"autopilotConfirmation"`.

    ```html
    <table class="gpii-fd-confirm-table">
       
        //more content not shown here
        
        <tr>
            td class="gpii-fd-confirm-table-name"><span id="newPreferenceLabel"></span></td>
            <td class="gpii-fd-confirm-table-value"><span id="newPreferenceConfirmation"></span></td>
            </tr>
        </tr>
                   
        //more content not shown here
            
    </table>
    ```
    
    After completing the previous step, your new "Autopilot" preference should appear in its own panel, and the correct value should appear in the preferences table on the confirmation panel.