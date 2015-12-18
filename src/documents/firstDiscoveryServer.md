---
title: First Discovery Server
layout: default
category: Overview
---

The First Discovery Server acts as a web server for a  [First Discovery Editor](https://github.com/GPII/first-discovery) instance and provides a means for storing preferences to the [GPII](http://gpii.net) Preferences server. While the First Discovery Server is built with [gpii-express](https://github.com/gpii/gpii-express) and is not actually a [Kettle](https://github.com/amb26/kettle/blob/KETTLE-32/README.md) application, it does makes use of Kettle features for creating [datasources](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#datasources), [configuration](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#structure-of-a-kettle-config), and for [starting](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#starting-a-kettle-application) the server.

Access to the GPII Preferences Server is mediated by the [GPII OAuth2 Security layer](https://wiki.gpii.net/w/GPII_OAuth_2_Guide). The First Discovery Server, communicates with the Security layer via the [Client Credentials Grant](https://wiki.gpii.net/w/GPII_OAuth_2_Guide#Client_Credentials_Grant) workflow.


## Configuration ##

The First Discovery Server can be configured via [Kettle Configs](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#structure-of-a-kettle-config). A set of these are provided with the server in the [config](https://github.com/GPII/first-discovery-server/tree/master/src/config) directory. An integrator can choose to make use of the provide configs directly or use them as the basis for creating new configs.

The [`gpii.firstDiscovery.server.configurator`](https://github.com/GPII/first-discovery-server/src/js/firstDiscoveryServer.js) grade defines a default schema for which the configuration is validated against. If the validation fails, the application will throw and error.

### environment.json ###

Accepts environment variables for all of the critical configuration options that are needed for running the First Discovery Server and connecting to the OAuth2 security server.

(see: [environment.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/environment.json))

<table>
    <thead>
        <tr>
            <th>Option</th>
            <th>Environment Variable</th>
            <th>Description</th>
            <th>Example</th>
        <tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>"port"</code>
            </td>
            <td>
                <code>FIRST_DISCOVERY_SERVER_TCP_PORT</code>
            </td>
            <td>
                The port number that the First Discovery Server is hosted at.
            </td>
            <td>
                "8088"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.securityServer.port"</code>
            </td>
            <td>
                <code>GPII_OAUTH2_TCP_PORT</code>
            </td>
            <td>
                The port number that the GPII OAuth2 server is hosted at.
            </td>
            <td>
                "8081"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.securityServer.hostname"</code>
            </td>
            <td>
                <code>GPII_OAUTH2_HOST_NAME</code>
            </td>
            <td>
                The hostname that the GPII OAuth2 server is hosted at.
            </td>
            <td>
                "http://localhost"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.securityServer.paths.token"</code>
            </td>
            <td>
                <code>GPII_OAUTH2_ACCESS_TOKEN_PATH</code>
            </td>
            <td>
                The path to the resource for requesting an access token
            </td>
            <td>
                "/access_token"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.securityServer.paths.preferences"</code>
            </td>
            <td>
                <code>GPII_OAUTH2_ADD_PREFERENCES_PATH</code>
            </td>
            <td>
                The path to the resource for creating a preference set.
                A query parameter can be added to provide the view/ontology that the
                preferences are to be stored in.
            </td>
            <td>
                "/add-preferences?view=%view"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.authentication.grant_type"</code>
            </td>
            <td>
                <code>GPII_OAUTH2_AUTH_GRANT_TYPE</code>
            </td>
            <td>
                The grant type supported by the OAuth2 server.
            </td>
            <td>
                "client_credentials"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.authentication.scope"</code>
            </td>
            <td>
                <code>GPII_OAUTH2_AUTH_SCOPE</code>
            </td>
            <td>
                The level of permissions that are being requested.
            </td>
            <td>
                "add_preferences"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.authentication.client_id"</code>
            </td>
            <td>
                <code>GPII_OAUTH2_AUTH_CLIENT_ID</code>
            </td>
            <td>
                The client ID registered with the OAuth2 server.
                Should be kept confidentially.
            </td>
            <td>
                "client_id_first_discovery"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.authentication.client_secret"</code>
            </td>
            <td>
                <code>GPII_OAUTH2_AUTH_CLIENT_SECRET</code>
            </td>
            <td>
                The client secret registered with the OAuth2 server.
                Used to securely identify the client with the OAuth2.
                Should be kept confidentially.
            </td>
            <td>
                "client_secret_first_discovery"
            </td>
        </tr>
    </tbody>
</table>

### oauth2.json ###

Builds on [environment.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/environment.json), setting concrete values to configuration of the OAuth2 server that are known to exists for the GPII security layer.

(see: [oauth2.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/oauth2.json))

<table>
    <thead>
        <tr>
            <th>Option</th>
            <th>Description</th>
            <th>Value</th>
        <tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>"preferencesConfig.securityServer.paths.token"</code>
            </td>
            <td>
                The path to the resource for requesting an access token
            </td>
            <td>
                "/access_token"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.securityServer.paths.preferences"</code>
            </td>
            <td>
                The path to the resource for creating a preference set.
                A query parameter can be added to provide the view/ontology that the
                preferences are to be stored in.
            </td>
            <td>
                "/add-preferences?view=%view"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.authentication.grant_type"</code>
            </td>
            <td>
                The grant type supported by the OAuth2 server.
            </td>
            <td>
                "client_credentials"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.authentication.scope"</code>
            </td>
            <td>
                The level of permissions that are being requested.
            </td>
            <td>
                "add_preferences"
            </td>
        </tr>
    </tbody>
</table>

### vagrant.json ###

Builds on [environment.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/environment.json) and [oauth2.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/oauth2.json), setting concrete values to configuration of the OAuth2 server that are expected when being run in a  [Vagrant VM](https://www.vagrantup.com). The configuration assumes that an instance of the OAuth2 server is available through the host machine at port 8081.

A Vagrant VM is provided with the First Discovery Server for quickly creating its own [development environment](https://github.com/GPII/first-discovery-server/blob/master/README.md#development).

(see: [vagrant.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/vagrant.json))

<table>
    <thead>
        <tr>
            <th>Option</th>
            <th>Description</th>
            <th>Example</th>
        <tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>"preferencesConfig.securityServer.port"</code>
            </td>
            <td>
                The port number that the GPII OAuth2 server is hosted at.
            </td>
            <td>
                "8081"
            </td>
        </tr>
        <tr>
            <td>
                <code>"preferencesConfig.securityServer.hostname"</code>
            </td>
            <td>
                The hostname that the GPII OAuth2 server is hosted at.
            </td>
            <td>
                "http://10.0.2.2"
            </td>
        </tr>
    </tbody>
</table>

## Launching ##

The First Discovery Server can be launched as a [Kettle](https://github.com/amb26/kettle/blob/KETTLE-32/README.md) application by making use of [Kettle Configs](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#structure-of-a-kettle-config).

There are two typical ways of launching a Kettle app, programmatically and from command line.

(See: [Starting a Kettle application](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#starting-a-kettle-application))

### Programmatically ###

```javascript
// require the kettle module
var kettle = require("kettle");

// load the config
kettle.config.loadConfig({
    // path to the config directory
    configPath:"./src/config",

    // name of the config to load, without the file extension
    configName: "vagrant"
});
```

### Command Line ####

```bash
# Call Kettle's init.js script with the
# configPath and configName
# node node_modules/kettle/init.js <configPath> [<configName>]
node node_modules/kettle/init.js ./src/config vagrant

# or using an environment variable to specify
# the configName
# NODE_EVN=<configName> node node_modules/kettle/init.js <configPath>
NODE_EVN=vagrant node node_modules/kettle/init.js ./src/config
```

## REST API ##

<table>
    <thead>
        <tr>
            <th>URL</th>
            <th>Request</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>/user[?view=:view]</code></td>
            <td><code>POST</code></td>
            <td>
                Accepts a set of preferences, in a JSON object, to be stored on the preferences server. For example:

                <pre>
                    <code>
{
  "gpii_firstDiscovery_language": "en-US"
}
                    </code>
                </pre>

                On successfully storing the preferences set, a JSON object is returned containing `userToken` and `preferences` properties. The `userToken` is the GPII token, which can be used for retrieving the preferences on a GPII enabled device. The `preferences` are a confirmation of the preferences stored on Preferences server for that GPII token. For example:

                <pre>
                    <code>
{
  "userToken": "2288e676-d0bb-4d29-8131-7cff268ba012",
  "preferences": {
    "contexts": {
      "gpii-default": {
        "name": "Default preferences",
        "preferences": {
          "gpii_firstDiscovery_language": "en-US"
        }
      }
    }
  }
}
                    </code>
                </pre>

                The optional <code>view</code> query parameter is used to specify which ontology the preferences are stored in. (See: <a href="https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md#post-preferencesviewview">Preferences Server</a>)
            </td>
        </tr>
    </tbody>
</table>

## Demos

This demo implements the integration with the [GPII Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md) to save preferences.
http://build.fluidproject.org/first-discovery/demos/prefsServerIntegration

## Source code

* [Client (First Discovery Tool)](https://github.com/GPII/first-discovery)
* [Server (First Discovery Server) - under development](https://github.com/GPII/first-discovery-server)
* [GPII Preferences Server](https://github.com/GPII/universal)
