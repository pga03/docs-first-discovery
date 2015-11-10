---
title: More complicated: Adding a simple preference
layout: default
category: Tutorials
---

Your flying car has an auto-pilot feature, and you want to add a preference for this. It’s a boolean preference, i.e. "Do you want auto-pilot turned on by default?" with a simple yes/no answer.

## Quick version

1. Edit `src/schemas/schemas.js` to add the actual preference to the primary schemas.
2. Create JSON files in the messages folder with the necessary strings.
3. Edit `demos/index.html` to add icon at bottom.
4. Edit `src/html/firstDiscovery.html` to add a placeholder for the panel.
5. Edit `src/css/style.css` to add styles for the icon and panel.
6. Create a JavaScript file for the code that creates the panel.
7. Link to the new JavaScript file in `demos/index.html`.
8. Edit `src/schemas/schemas.js` to add code for the panel to auxiliary schema.

## Detailed Instructions

1. Edit `src/schemas/schemas.js` to add the actual preference to the primary schemas.

    A. The `src/schemas/schemas.js` file contains the primary schema, which defines the preferences, and the auxiliary schema, which defines the editor itself (i.e. the panels used to adjust the preferences, where to find HTML templates, etc.)

    You can see the entire file here: https://github.com/GPII/first-discovery/blob/master/src/schemas/schemas.js

    B. In the `schemas.js` file, find the definition of the `"speak"` primary schema, which start with `fluid.defaults("gpii.firstDiscovery.schemas.speak", `:

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

    This preference is a boolean preference, just like the auto-pilot preference we want to add.

    C. Add a new definition that takes the same form as the `"speak"` preference, but with `"autoPilot"` instead of `"speak"`. Change the default value to false (since we probably don’t want the car to just start out with auto-pilot on):

    ```javascript
    fluid.defaults("gpii.firstDiscovery.schemas.autoPilot", {
        gradeNames: ["fluid.prefs.schemas"],
            schema: {
              "gpii.firstDiscovery.autoPilot": {
                   "type": "boolean",
                    "default": false
                }
            }
    });
    ```

2. Create JSON files in the src/messages folder with the necessary strings.

    A. The src/messages folder contains JSON files containing the interface strings for each preference panel. The file "speakText_en-US.json" is an example of the form of message file you’ll create for your preference panel.

    You can see that file here: https://github.com/GPII/first-discovery/blob/master/src/messages/speakText_en-US.json

    B. Create a new file in the messages folder called "autoPilot_en-US.json".

    C. Edit the contents of the file according to the auto-pilot functionality:
    * Define the "instructions" as "Do you want auto-pilot turned on by default?";
    * Define the "yes-tooltip" as "Select to turn auto-pilot on";
    * Define the "no-tooltips"Select to turn auto-pilot off";
    * Define the "yes-tooltipAtSelect" as "Auto-pilot is on";
    * Define the "no-tooltipAtSelect" as "Auto-pilot is off".

    ```javascript
    {
        "instructions": "Do you want auto-pilot turned on by default?",
        "no": "No",
        "yes": "Yes",

        "yes-tooltip": "Select to turn auto-pilot on",
        "no-tooltip": "Select to turn auto-pilot off",
        "yes-tooltipAtSelect": "Auto-pilot is on",
        "no-tooltipAtSelect": "Auto-pilot is off"
    }
    ```

    D. Duplicate the file for other languages; for example, create a file called "autoPilot_fr-FR.json" for a French version. Use exactly the same keys in the file, but change the values to the translated strings:

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

3. Edit `demos/index.html` and the CSS to add icon at bottom.

    A. In the `demos/index.html` file, find the list of icons (a `<ul>` with the class "gpii-fd-navIcon-outer"  as described above).

    B. Add a new `<li>` element of the same form as the others, but define the preference-specific class name to reflect the auto-pilot preference:

    ```html
    <ul class="gpii-fd-navIcon-outer">
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-lang">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon-welcome">
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-showSounds">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-autoPilot">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
        <li class="gpiic-fd-navIcon gpii-fd-navIcon gpii-fd-volume">
            <div class="gpiic-fd-activeIndicator gpii-fd-activeIndicator"></div>
            <div class="gpiic-fd-confirmedIndicator gpii-fd-confirmedIndicator"></div>
        </li>
           <!-- some list items not shown -->
    </ul>
    ```

    Note that only the last class name on the `<li>` itself has changed.

4. Edit `src/html/firstDiscovery.html` to add a placeholder for the panel.

    A. Add a new `<section>` element of the same form as the others, but define the class names to reflect the auto-pilot preference:

    ```html
    <section class="gpiic-fd-prefsEditor-panel-lang gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-lang gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-welcome gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-welcome gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-showSounds gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-showSounds gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-autoPilot gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-autoPilot gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speakText gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speakText gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-speechRate gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-speechRate gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-size gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-size gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-keyboard gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-keyboard gpii-fd-main"></section>
    <section class="gpiic-fd-prefsEditor-panel-congratulations gpiic-fd-prefsEditor-panel gpii-fd-prefsEditor-panel-congratulations gpii-fd-main"></section>
    ```

    Make sure that the new `<section>` element places the panel in the correct order: the same as the navigation icons in demos/index.html.

5. Edit `src/css/style.css` to add styles for the icon and panel.

    A. The icons at the bottom of the screen are implemented in CSS, using an icon font. These instructions assume you are familiar with icon fonts and will use them for your new panel. For information about creating and usin icon fonts, see http://docs.fluidproject.org/infusion/development/tutorial-creatingANewAdjusterUI/HowToCreateAndUseFontIcons.html

    You can see the entire CSS file here: https://github.com/GPII/first-discovery/blob/master/src/css/style.css

    B. The icon characters are added as content to the document using the :before selector and the content property, as seen in the CSS for the language icon:

    ```css
    .gpii-fd-lang:before {
        content: "\e608";
    }
    ```

    C. Create a style for your new icon, using the class name defined in step 3, and set the content to the character code for your desired icon (this example will use "\e700" just as an example – no such character exists currently in the icon font; you must use the correct character code for the icon you want to use).

    ```css
    .gpii-fd-autoPilot:before {
        content: "\e700";
    }
    ```

6. Create a JavaScript file for the code that creates the panel.

    A. Create a new JavaScript file in the src/js folder called newPanels.js. Create a closure for your code:

    ```javascript
    (function ($, fluid) {
        // your code will go here
    })(jQuery, fluid_2_0);
    ```

    A _closure_ wraps the code in an anonymous function. This separates private and public functions: Only objects or functions that are attached to the global namespace object will be publicly available. Anything else inside the anonymous function will be invisible to the rest of the world.

    D. Inside the closure use a call to fluid.defaults() to create the panel, which we’ll call "gpii.firstDiscovery.panel.autoPilot":

    ```javascript
    (function ($, fluid) {
        fluid.defaults("gpii.firstDiscovery.panel.autoPilot", {
            // configuration options will go here
        });
    })(jQuery, fluid_2_0);
    ```

    `fluid.defaults()` is one of the core functions in Infusion: It is used to create components (the building blocks of any Infusion application) and register them with the Framework.

    E. Fill in the configuration options for the panel:

    The First Discovery Tool currently presents four basic ‘styles’ of preference: 1) basic yes/no questions, 2) a range of values (like the text size), 3) a set of choices (like the colour combinations), and 4) the keyboard adjustments.

    The code for the First Discovery Tool includes some base grades that can be used to implement a panel of one of these types (including the HTML template, and the CSS for styling). These base grades define most of the functionality for a particular type of panel; using these grades will effectively ‘inherit’ this functionality.

    For a boolean preference, the First Discovery Tool has a grade called gpii.firstDiscovery.panel.yesNo that provides most of the functionality for a simple yes/no panel:

    ```javascript
    (function ($, fluid) {
        fluid.defaults("gpii.firstDiscovery.panel.autoPilot", {
            gradeNames: ["gpii.firstDiscovery.panel.yesNo"],
            // more options will go here
        });
    })(jQuery, fluid_2_0);
    ```

    (You will see in the code that other panel types have different grades specified in the gradeNames option.)
    Every panel needs a preferenceMap option to tell the framework how to map the preference in the Primary Schema to the Panel:

    ```javascript
    (function ($, fluid) {
        fluid.defaults("gpii.firstDiscovery.panel.autoPilot", {
            gradeNames: ["gpii.firstDiscovery.panel.yesNo"],
            preferenceMap: {
                "gpii.firstDiscovery.autoPilot": {
                    "model.value": "default"
                }
            }
        });
    })(jQuery, fluid_2_0);
    ```

7. Link to the new JavaScript file in `demos/index.html`.

    A. Add a `<script>` link to the new JavaScript file in the head of demos/index.html:

    ```html
    <script type="text/javascript" src="../src/js/nav.js`></script>
    <script type="text/javascript" src="../src/js/firstDiscoveryEditor.js`></script>
    <script type="text/javascript" src="js/demos.js`></script>
    <script type="text/javascript" src="js/newPanels.js`></script>

    <title>First Discovery Tool</title>
    ```

8. Edit `src/schemas/schemas.js` to add code for panel to the auxiliary schema.

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

    C. Inside the section named "auxiliarySchema", add a section for the new panel:

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
            "autoPilot": {
                "type": "gpii.firstDiscovery.autoPilot",
                "panel": {
                    "type": "gpii.firstDiscovery.panel.autoPilot",
                    "container": ".gpiic-fd-prefsEditor-panel-autoPilot",
                    "template": "%templatePrefix/yesNo.html",
                    "message": "%messagePrefix/autoPilot.json"
                }
            },
            // more content not shown
        }
    });
    ```

