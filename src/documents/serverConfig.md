---
title: Configuring the connection to the Preferences Server
layout: default
category: Tutorials
---

The First Discovery Tool includes grades and components that can be used to save preferences to the
[GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md).

This tutorial describes how to customize the URL that the preferences are sent to and method.

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

