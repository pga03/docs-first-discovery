---
title: Advanced: Configuring the connection to the Preferences Server
layout: default
category: Tutorials
---

This tutorial explains how the First Discovery Tool connects to the
[GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md).

## Background

Broadly speaking, the configuration of the First Discovery Tool (and of any preferences editor
created with the
[Preferences Framework](http://docs.fluidproject.org/infusion/development/PreferencesFramework.html)
) is configured through an
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

## Alternative Auxiliary Schema

This basic configuration of the First Discovery Tool does _not_ connect to a preferences server,
but the Tool includes an alternative Auxiliary Schema, the "Preferences Server Integration schema",
that can be used to make this connection.

The Preferences Server Integration schema is defined alongside the default schema, in the
[schemas.js file](https://github.com/GPII/first-discovery/blob/master/src/schemas/schemas.js):

```javascript
fluid.defaults("gpii.firstDiscovery.auxSchema.prefsServerIntegration", {
    // using the base auxSchema as the grade inherits everything in there
    gradeNames: ["gpii.firstDiscovery.auxSchema"],

    auxiliarySchema: {

        // add the extra grade to the loader grades
        "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor",
                         "gpii.firstDiscovery.prefsServerIntegration"],

        // add the token panel
        "token": {
            "type": "gpii.firstDiscovery.token",
            "panel": {
                "type": "gpii.firstDiscovery.panel.token",
                "container": ".gpiic-fd-prefsEditor-panel-token",
                "template": "%templatePrefix/token.html",
                "message": "%messagePrefix/token.json"
            }
        },

        // override the original template to add the extra panel placeholder
        "template": "%templatePrefix/firstDiscoveryPrefsServerIntegration.html",

        // customize the text on the congratulations panel
        "congratulations": {
            "panel": {
                "message": "%messagePrefix/congratulationsPrefsServerIntegration.json"
            }
        }
    }
});
```

This schema makes two key changes to the auxiliary schema:
* It adds a [Preferences Server Integration](prefsServerIntegration.md) grade to the `loaderGrades`.
This grade sets up the connection between the Token Panel (see below) and the rest of the tool.
* It adds a [Token Panel](token.md) to the set of panels. This panel transmits the preferences
to the server and receives, in return, a unique token that is displayed and
can be used to retrieve the preferences later.

In addition to these changes, this schema makes two more changes to support different messages
in the interface:
* It overrides the default `template` with an alternative template containing a placeholder for
the new Token Panel at the end of the process.
* It overrides the default message file for the `congratulations` panel with an alternative
message file containing information about the saving of preferences.

## Using the Alternative Schema

To instantiate the First Discovery Tool using the Preferences Server Integration schema, provide
the schema name in the call to
[`fluid.prefs.create()`](http://docs.fluidproject.org/infusion/development/PreferencesEditor.html)
instead of the default schema:

```javascript
fluid.prefs.create(container, {
    build: {
        gradeNames: ["gpii.firstDiscovery.auxSchema.prefsServerIntegration"]
    }
});
```

### Overriding Paths

The default
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html)
provided with the First Discovery Tool specifies root paths to
the templates and message bundles used by the First Discovery Tool. These paths are relative, so an
integration will likely need to override them. To do this:

1. Create a custom Auxiliary Schema that uses the `prefsServerIntegration` schema and
overrides the `terms` property, which specifies the paths:

    ```javascript
    fluid.defaults("my.auxSchema.prefsServerIntegration", {
        gradeNames: ["gpii.firstDiscovery.auxSchema.prefsServerIntegration"],
        auxiliarySchema: {
            "terms": {
                // path to templates and messages, relative to where this FD tool is
                "templatePrefix": "my/relative/path/to/first-discovery/src/html",
                "messagePrefix": "my/relative/path/to/first-discoverysrc/messages"
            }
        }
    });
    ```

2. Use this custom schema in the instantiation of the Tool:

    ```javascript
    fluid.prefs.create(container, {
        build: {
            gradeNames: ["my.auxSchema.prefsServerIntegration"]
        }
    });
    ```

### Configuring the Preferences Server Connection

The [Token Panel](token.md), which saves the preferences to the preferences server, uses a default URL that
assumes that the preferences server is at the same base URL as the First Discovery Tool itself.
It's likely that this won't be case, and that you'll need to specify a different URL. To do this:

1. Create a grade that defines the server configuration options you want.

    This grade should use `fluid.component` as its base grade and provide the
    [`saveRequestConfig` option](token.md#options)
    required by the Token Panel:

    ```javascript
    fluid.defaults("my.serverConfig", {
        gradeNames: ["fluid.component"],
        saveRequestConfig: {
            url: "http://my.host/myServer/user",
            method: "POST",
            view: "myApp"
        }
    });
    ```

2. Add your grade to the `loaderGrades` in the
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html).

    Note that all of the desired loader grades must be included in the `loaderGrades` property,
    not just the new one that you are adding.

    ```javascript
    fluid.defaults("my.auxSchema.prefsServerIntegration", {
        gradeNames: ["gpii.firstDiscovery.auxSchema.prefsServerIntegration"],
        auxiliarySchema: {
            "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor",
                             "gpii.firstDiscovery.prefsServerIntegration",
                             "my.serverConfig"],
            "terms": {
                // new paths to templates and messages
                "templatePrefix": "my/path/to/first-discovery/src/html",
                "messagePrefix": "my/path/to/first-discovery/src/messages"
            }
        }
    });
    ```

3. Use this custom schema in the instantiation of the Tool:

    ```javascript
    fluid.prefs.create(container, {
        build: {
            gradeNames: ["my.auxSchema.prefsServerIntegration"]
        }
    });
    ```




