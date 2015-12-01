---
title: The Work Flow
layout: default
category: Overview
---

The process of saving preferences to the [GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md) is as follows:

1. The First Discovery Tool sends a POST request to the First Discovery Server at `/user?view=firstDiscovery`. The body of the request is a JSON string of user selected preferences, for example:
    ```javascript
    {
        fluid_prefs_contrast: "default"
        fluid_prefs_textSize: 1
        gpii_firstDiscovery_captions: true
        gpii_firstDiscovery_language: "en-US"
        gpii_firstDiscovery_onScreenKeyboard: true
        gpii_firstDiscovery_showSounds: false
        gpii_firstDiscovery_speak: false
        gpii_firstDiscovery_speechRate: 1
        gpii_firstDiscovery_stickyKeys: false
    }
    ```

2. The First Discovery Server receives user selected preferences, follows [OAuth2 Client Credentials Grant API](https://wiki.gpii.net/w/GPII_OAuth_2_Guide#Client_Credentials_Grant) provided by the GPII Preferences Server to save preferences to the GPII Preferences Server;

3. The GPII Preferences Server saves the preferences, generates and responds to the First Discovery Server with a token that identifies the saved preferences;

4. The First Discovery Server responds to the request that the First Discovery Tool sends in step 1 with the token returned by the GPII Preferences Server. An example of a GPII token:
    ```2288e676-d0bb-4d29-8131-7cff268ba012```
