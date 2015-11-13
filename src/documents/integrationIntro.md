---
title: Preferences Server Integration
layout: default
category: Overview
---

The First Discovery Tool is integrated with the [GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md) to save user selected preferences. The users of The First Discovery Tool are usually new to the concept of preferences that can be used to customize a user interface to match their needs. They normally don't have an existing ID with the GPII Preferences Server. This integration saves user selected preferences to the GPII Preferences Server and the GPII Preferences Server returns a token that can be kept and used to retrieved the save preferences when needed. The returned token is essentially this user's newly-created user IDs with the GPII Preferences Server.

*Note*: The First Discovery Tool potentially can be integrated with any preferences servers that support the save of user preferences. This document only explains how it integrates with the GPII Preferences Server.

## The First Discovery Server

The First Discovery Tool makes use of [OAuth2 Client Credentials Grant API](https://wiki.gpii.net/w/GPII_OAuth_2_Guide#Client_Credentials_Grant) provided by the [GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md) to adds preferences. [OAuth2 Client Credentials Grant API](https://wiki.gpii.net/w/GPII_OAuth_2_Guide#Client_Credentials_Grant) requires the client ID and secret to be included in the http request for OAuth2 authentication. For the security reason, these information should only be sent between servers, instead of between browsers to the GPII Preferences Server. This is why the First Discovery Server is needed. The First Discovery Server basically sends http requests to add preferences on behalf of users of the First Discovery Tool. What it does:

* Serve the First Discovery Tool
* Receive http requests sent from the First Discovery Tool. These requests only contain user selected preferences
* Follow [OAuth2 Client Credentials Grant API](https://wiki.gpii.net/w/GPII_OAuth_2_Guide#Client_Credentials_Grant) to send user selected preferences to the [GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md)
* Send back the GPII token returned by the [GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md) to the First Discovery Tool 

## Demos

Preferences Server Integration: http://build.fluidproject.org/first-discovery/demos/prefsServerIntegration (doesn't yet return a token)

## Source code

Client (First Discovery Tool): https://github.com/GPII/first-discovery
Server (First Discovery Server): https://github.com/GPII/first-discovery-server (under development)
GPII Preferences Server: https://github.com/GPII/universal
