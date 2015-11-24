---
title: First Discovery Server
layout: default
category: Overview
---

## Configuration ##

### Host Port ###

By default the server will run from port 8088, but can be configured to use a different port by setting the `FIRST_DISCOVERY_SERVER_TCP_PORT` environment variable to a different port number.


### Preferences Server Communication ###

The First Discovery Server connects to the Preferences Server via the Security layer. The server-to-server communication needs to be configured to specify things such as hostname, port, client_id, client_secret and etc.

Configuration can be provided using either environment variables or a JSON config file. In the event that both are provided, the environment variables will take precedence.

#### Environment Variables ####

<table>
    <thead>
        <tr>
            <th>Environment Variable</th>
            <th>Description</th>
            <th>Example</th>
        <tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>GPII_OAUTH2_TCP_PORT</code>
            </td>
            <td>
                The port number that the GPII Oauth2 server is hosted at.
            </td>
            <td>
                "8088"
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_HOST_NAME</code>
            </td>
            <td>
                The hostname that the GPII Oauth2 server is hosted at.
            </td>
            <td>
                "http://localhost"
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_PATH_ACCESS_TOKEN</code>
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
                <code>GPII_OAUTH2_PATH_ADD_PREFERENCES</code>
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
                <code>GPII_OAUTH2_AUTH_GRANT_TYPE</code>
            </td>
            <td>
                The grant type supported by the Oauth2 server.
            </td>
            <td>
                "client_credentials"
            </td>
        </tr>
        <tr>
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
                <code>GPII_OAUTH2_AUTH_CLIENT_ID</code>
            </td>
            <td>
                The client ID registered with the Oauth2 server.
            </td>
            <td>
                "client_id_first_discovery"
            </td>
        </tr>
        <tr>
            <td>
                <code>GPII_OAUTH2_AUTH_CLIENT_SECRET</code>
            </td>
            <td>
                The client secret registered with the Oauth2 server.
                Used to securely identify the client with the Oauth2.
            </td>
            <td>
                "client_secret_first_discovery"
            </td>
        </tr>
    </tbody>
</table>

#### Configuration File ####

The configuration file must be called "fd_security_config.json" and be located in the server's
root directory.

<table>
    <thead>
        <tr>
            <th>Path</th>
            <th>Description</th>
            <th>Example</th>
        <tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>securityServer.port</code>
            </td>
            <td>
                The port number that the GPII Oauth2 server is hosted at.
            </td>
            <td>
                "8088"
            </td>
        </tr>
        <tr>
            <td>
                <code>securityServer.hostname</code>
            </td>
            <td>
                The hostname that the GPII Oauth2 server is hosted at.
            </td>
            <td>
                "http://localhost"
            </td>
        </tr>
        <tr>
            <td>
                <code>securityServer.paths.token</code>
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
                <code>securityServer.paths.preferences</code>
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
                <code>authentication.grant_type</code>
            </td>
            <td>
                The grant type supported by the Oauth2 server.
            </td>
            <td>
                "client_credentials"
            </td>
        </tr>
        <tr>
            <td>
                <code>authentication.scope</code>
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
                <code>authentication.client_id</code>
            </td>
            <td>
                The client ID registered with the Oauth2 server.
            </td>
            <td>
                "client_id_first_discovery"
            </td>
        </tr>
        <tr>
            <td>
                <code>authentication.client_secret</code>
            </td>
            <td>
                The client secret registered with the Oauth2 server.
                Used to securely identify the client with the Oauth2.
            </td>
            <td>
                "client_secret_first_discovery"
            </td>
        </tr>
    </tbody>
</table>

##### Example #####

```JSON
{
    "securityServer": {
        "port": "8081",
        "hostname": "http://10.0.2.2",
        "paths": {
            "token": "/access_token",
            "preferences": "/add-preferences?view=%view"
        }
    },
    "authentication": {
        "grant_type": "client_credentials",
        "scope": "add_preferences",
        "client_id": "client_id_first_discovery",
        "client_secret": "client_secret_first_discovery"
    }
}
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
            <td><code>/demos/...<code></td>
            <td><code>GET</code></td>
            <td>
                The First Discovery Tool's demos are served up from this root directory. The exact path to files will depend on the structure of the demos.
                <em>(See: <a href="https://github.com/gpii/first-discovery">first-discovery</a>)</em>
            </td>
        </tr>
        <tr>
            <td><code>/src/...<code></td>
            <td><code>GET</code></td>
            <td>
                Serves the dependencies required by the First Discovery Tool's demos. Typically these resources will not needed to be accessed directly.
            </td>
        </tr>
        <tr>
            <td><code>/user?[view=:view]</code></td>
            <td><code>POST</code></td>
            <td>
                Accepts a set of preferences, in a JSON object, to be stored on the preferences server. For example:

                <code>
                    <pre>
{
    "gpii_firstDiscovery_language": "en-US"
}
                    </pre>
                </code>

                A GPII token will be returned and can be used for retrieving the preferences on a GPII enabled device. For example:

                <code>
                    <pre>
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
                    </pre>
                </code>

                The <code>view</code> query parameter is used to specify which ontology the preferences are stored in. (See: <a href="https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md#post-preferencesviewview">Prefrences Server</a>)
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
