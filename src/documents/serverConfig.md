---
title: Advanced: Configuring the connection to the Preferences Server
layout: default
category: Tutorials
---

This tutorial explains how the First Discovery Tool connects to the
[GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md).
It introduces some functionality of
[Infusion](http://fluidproject.org/infusion.html)
and its
[Preferences Framework](http://docs.fluidproject.org/infusion/development/PreferencesFramework.html).

----

Broadly speaking, the configuration of the First Discovery Tool (and of any preferences editor
created with the Preferences Framework) is configured through an
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html).
This is a JSON document that specifies configuration information such as what panels to show,
where to find HTML templates, and other things.

The basic First Discovery Tool is configured through the default Auxiliary Schema, which can be
seen in the
[schemas.js file](https://github.com/GPII/first-discovery/blob/master/src/schemas/schemas.js):
```javascript
fluid.defaults("gpii.firstDiscovery.auxSchema", {
    gradeNames: ["fluid.prefs.auxSchema"],
    auxiliarySchema: {
        // schema details not shown here
    }
});
```

This basic configuration of the First Discovery Tool does _not_ connect to a preferences server.
The Tool includes an alternative Auxiliary Schema that customizes the default schema, adding the
necessary bits and pieces. This alternative schema is also defined in the
[schemas.js file](https://github.com/GPII/first-discovery/blob/master/src/schemas/schemas.js):
```javascript
fluid.defaults("gpii.firstDiscovery.auxSchema.prefsServerIntegration", {
    // using the base auxSchema as the grade inherits everything in there
    gradeNames: ["gpii.firstDiscovery.auxSchema"],

    auxiliarySchema: {

        // add the extra grade to the loader grades
        "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor", "gpii.firstDiscovery.prefsServerIntegration"],

        // override the original template to add the extra panel placeholder
        "template": "%templatePrefix/firstDiscoveryPrefsServerIntegration.html",

        // customize the text on the congratulations panel
        "congratulations": {
            "panel": {
                "message": "%messagePrefix/congratulationsPrefsServerIntegration.json"
            }
        },

        // add the token panel
        "token": {
            "type": "gpii.firstDiscovery.token",
            "panel": {
                "type": "gpii.firstDiscovery.panel.token",
                "container": ".gpiic-fd-prefsEditor-panel-token",
                "template": "%templatePrefix/token.html",
                "message": "%messagePrefix/token.json"
            }
        }
    }
});
```

This special preferences server integration schema uses two components that work together to save
the user's preferences to the Preferences Server at the end of the First Discovery Process:
1. the [Token Panel](token.md), which transmits the preferences to the server and receives,
in return, a unique token that can be used to retrieve the preferences later, and
2. a [Preferences Server Integration](prefsServerIntegration.md) grade that
sets up the connection between the Token Panel and the rest of the tool.

----

## Quick version
1. Create a grade that defines the server configuration options you want.
2. Add your grade to the `loaderGrades` in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html).

## Detailed Instructions

1. Create a grade that defines the server configuration options you want.

    A. asdf

    ```javascript
    fluid.defaults("gpii.firstDiscovery.myServerConfig", {
        gradeNames: ["fluid.component"],
        saveRequestConfig: {
            url: "http://my.host/myServer/user",
            method: "POST"
        }
    });
    ```

    B. asdf.

2. Add your grade to the `loaderGrades` in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html).

    A. asdf

    ```javascript
    fluid.defaults("my.prefsEditor", {
        gradeNames: ["gpii.firstDiscovery.auxSchema"],
        auxiliarySchema: {
            "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor",
                            "gpii.firstDiscovery.prefsServerIntegration",
                            "gpii.firstDiscovery.myServerConfig"],
    ```

    B. asdf.

