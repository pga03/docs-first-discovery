---
title: First Discovery Server
layout: default
category: Overview
---

The First Discovery Server acts as a web server for a  [First Discovery Editor](https://github.com/GPII/first-discovery) instance and provides a means for storing preferences to the [GPII](http://gpii.net) [Preferences Server](https://github.com/GPII/universal). The First Discovery Server makes use of the [Kettle configuration system](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#structure-of-a-kettle-config) for [configuration](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#structure-of-a-kettle-config) and [instantiation](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#starting-a-kettle-application), but uses [gpii-express](https://github.com/gpii/gpii-express) rather than [Kettle](https://github.com/amb26/kettle/blob/KETTLE-32/README.md) for expressing an HTTP server.

Access to the GPII Preferences Server is mediated by the [GPII OAuth2 Security layer](https://wiki.gpii.net/w/GPII_OAuth_2_Guide). The First Discovery Server communicates with the Security layer via the [Client Credentials Grant](https://wiki.gpii.net/w/GPII_OAuth_2_Guide#Client_Credentials_Grant) workflow.


## Configuration ##

The First Discovery Server can be configured via [Kettle Configs](https://github.com/amb26/kettle/blob/KETTLE-32/README.md#structure-of-a-kettle-config). A set of these are provided with the server in the [config](https://github.com/GPII/first-discovery-server/tree/master/src/config) directory. An integrator can choose to make use of the provided configs directly or use them as the basis for creating new configs.

The [`gpii.firstDiscovery.server.configurator`](https://github.com/GPII/first-discovery-server/tree/master/src/js/firstDiscoveryServer.js) grade defines a default schema which the configuration is validated against. If the validation fails, the application will throw an error.

### environment.json ###

[environment.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/environment.json) accepts environment variables for all of the critical configuration options that are needed for running the First Discovery Server and connecting to the OAuth2 security server.

<table>
    <thead>
        <tr>
            <th>Environment Variable</th>
            <th>Description</th>
        <tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>FIRST_DISCOVERY_SERVER_TCP_PORT</code>
            </td>
            <td>
                The port number that the First Discovery Server is hosted at.
                <p>
                    Example:
                    "8088"
                </p>
                <p>
                    Option Path:
                    <code>port</code>
                </p>
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_TCP_PORT</code>
            </td>
            <td>
                The port number that the GPII OAuth2 server is hosted at.
                <p>
                    Example:
                    "8081"
                </p>
                <p>
                    Option Path:
                    <code>preferencesConfig.securityServer.port</code>
                </p>
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_HOST_NAME</code>
            </td>
            <td>
                The hostname that the GPII OAuth2 server is hosted at.
                <p>
                    Example:
                    "http://localhost"
                </p>
                <p>
                    Option Path:
                    <code>preferencesConfig.securityServer.hostname</code>
                </p>
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_ACCESS_TOKEN_PATH</code>
            </td>
            <td>
                The path to the resource for requesting an access token.
                <p>
                    Example:
                    "/access_token"
                </p>
                <p>
                    Option Path:
                    <code>preferencesConfig.securityServer.paths.token</code>
                </p>
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_ADD_PREFERENCES_PATH</code>
            </td>
            <td>
                The path to the resource for creating a preference set.
                A query parameter can be added to provide the view/ontology that the
                preferences are to be stored in.
                <p>
                    Example:
                    "/add-preferences?view=%view"
                </p>
                <p>
                    Option Path:
                    <code>preferencesConfig.securityServer.paths.preferences</code>
                </p>
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_AUTH_GRANT_TYPE</code>
            </td>
            <td>
                The grant type supported by the OAuth2 server.
                <p>
                    Example:
                    "client_credentials"
                </p>
                <p>
                    Option Path:
                    <code>preferencesConfig.authentication.grant_type</code>
                </p>
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_AUTH_SCOPE</code>
            </td>
            <td>
                The level of permissions that are being requested.
                <p>
                    Example:
                    "add_preferences"
                </p>
                <p>
                    Option Path:
                    <code>preferencesConfig.authentication.scope</code>
                </p>
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_AUTH_CLIENT_ID</code>
            </td>
            <td>
                The client ID registered with the OAuth2 server.
                Should be kept confidentially.
                <p>
                    Example:
                    "client_id_first_discovery"
                </p>
                <p>
                    Option Path:
                    <code>preferencesConfig.authentication.client_id</code>
                </p>
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_AUTH_CLIENT_SECRET</code>
            </td>
            <td>
                The client secret registered with the OAuth2 server.
                Used to securely identify the client with the OAuth2.
                Should be kept confidentially.
                <p>
                    Example:
                    "client_secret_first_discovery"
                </p>
                <p>
                    Option Path:
                    <code>preferencesConfig.authentication.client_secret</code>
                </p>
            </td>
        </tr>
    </tbody>
</table>

### oauth2.json ###

[oauth2.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/oauth2.json) merges on top of  [environment.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/environment.json) to replace the authentication related environment variables with concrete values for the [Client Credentials Grant](https://wiki.gpii.net/w/GPII_OAuth_2_Guide#Client_Credentials_Grant) workflow.

<table>
    <thead>
        <tr>
            <th>Option Path</th>
            <th>Description</th>
            <th>Value</th>
        <tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>preferencesConfig.securityServer.paths.token</code>
            </td>
            <td>
                The path to the resource for requesting an access token.

                (see: [GPII OAuth 2 Guide: Access Token](https://wiki.gpii.net/w/GPII_OAuth_2_Guide#Step_1:_Request_an_access_token))
            </td>
            <td>
                "/access_token"
            </td>
        </tr>
        <tr>
            <td>
                <code>preferencesConfig.securityServer.paths.preferences</code>
            </td>
            <td>
                The path to the resource for creating a preference set.
                A query parameter can be added to provide the view/ontology that the
                preferences are to be stored in.

                (see: [GPII OAuth 2 Guide: User's Preferences](https://wiki.gpii.net/w/GPII_OAuth_2_Guide#Step_2:_Use_the_access_token_to_add_the_user.27s_preferences))
            </td>
            <td>
                "/add-preferences?view=%view"
            </td>
        </tr>
        <tr>
            <td>
                <code>preferencesConfig.authentication.grant_type</code>
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
                <code>preferencesConfig.authentication.scope</code>
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

[vagrant.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/vagrant.json) merges on top of   [oauth2.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/oauth2.json), replacing the environment variables for connecting to the OAuth2 server with the expect hostname and port when running inside of a [Vagrant VM]([Vagrant VM](https://www.vagrantup.com). The configuration assumes that an instance of the OAuth2 server is available through the host machine at port 8081.

A Vagrant VM is provided with the First Discovery Server for quickly creating its own [development environment](https://github.com/GPII/first-discovery-server/blob/master/README.md#development).

(see: [vagrant.json](https://github.com/GPII/first-discovery-server/tree/master/src/config/vagrant.json))

<table>
    <thead>
        <tr>
            <th>Option Path</th>
            <th>Description</th>
            <th>Value</th>
        <tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>preferencesConfig.securityServer.port</code>
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
                <code>preferencesConfig.securityServer.hostname</code>
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
# NODE_ENV=<configName> node node_modules/kettle/init.js <configPath>
NODE_ENV=vagrant node node_modules/kettle/init.js ./src/config
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
<code>{"gpii_firstDiscovery_language": "en-US"}</code>
                </pre>

                On successfully storing the preferences set, a JSON object is returned containing `userToken` and `preferences` properties. The `userToken` is the GPII token, which can be used for retrieving the preferences on a GPII enabled device. The `preferences` are a confirmation of the preferences stored on Preferences server for that GPII token. For example:

                <pre>

<code>{
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
}</code>
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
* [Server (First Discovery Server)](https://github.com/GPII/first-discovery-server)
* [GPII Preferences Server](https://github.com/GPII/universal/tree/master/gpii/node_modules/preferencesServer)
