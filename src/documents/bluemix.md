---
title: Advanced: Deploying First Discovery to Bluemix
layout: default
category: Tutorials
---
    
## Introduction    
You can get an internet accessible website serving the First Discovery Tool up and running with relative
ease using [IBM Bluemix](http://bluemix.net) and this tutorial will guide you through doing just that. 

## Requirements
This tutorial assumes you have the following software installed:

* [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Docker](https://docs.docker.com/engine/installation/)
* [Cloud Foundry command line interface](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
* [IBM Containers Plugin for Cloud Foundry](https://console.ng.bluemix.net/docs/containers/container_cli_ov.html)

If you need help with any of those try looking [here](https://developer.ibm.com/answers/questions/201537/how-to-install-the-prereqs-to-run-supported-ibm-co.html) for more information.
You should also have a [Bluemix account.](https://console.ng.bluemix.net/registration/)

## Overview of Components

First, lets go over the components involved. 

1. **First Discovery Tool** - this is the Infusion based client side app. It runs in your web browser.
2. **First Discovery Server** - this is the server side component that will serve up the First Discovery Tool and proxy requests to the GPII Flow Manager.


## Quick version
1. Login

        cf login -a https://api.ng.bluemix.net -o <orginization -s <space>
    
2. Init containers plugin:

        cf ic init
    
3. Set organization namespace: 

        cf ic namespace set <namespace>
    
4. Create a scratch space: 

        cf create-space tutorial && cf target -s tutorial
    
5. Build first discovery server image: 

        git clone https://github.com/GPII/first-discovery-server.git 
        cf ic build --rm=true --no-cache=true -t first_discovery_server first-discovery-server

6. Create the container group:

        cf ic group create \
            -p 8088 \
            --min 1 \
            --max 2 \
            --desired 1 \
            --memory 256 \
            --name first-discovery-group \
            -e NODE_ENV=bluemix \
            -e GPII_OAUTH2_AUTH_CLIENT_ID="net.gpii.prefsEditors.firstDiscovery" \
            -e GPII_OAUTH2_AUTH_CLIENT_SECRET="client_secret_firstDiscovery" \
            -e GPII_OAUTH2_HOST_NAME="<url for flow manager>" \       # use your initials to make the URL unique
            -e GPII_OAUTH2_TCP_PORT="80" \
            registry.ng.bluemix.net/<namespace>/first_discovery_server:latest                   # use your own namespace here

7. Map the route

        cf ic route map --hostname firstdiscovery-<your initials> --domain mybluemix.net first-discovery-group

8. Test
  
    Open the route `http://firstdiscovery-<your initials>.mybluemix.net/demos/prefsServerIntegration` in your browser. 

## Long Version
### Setup Bluemix, Cloud Foundry CLI, and IBM Containers

#### Login

Run the following commands to initialize your tools.

    cf login -a https://api.ng.bluemix.net -o <orginization -s <space>
    
Note: some examples in this tutorial require you to use values that are specific to you. These are noted in commands with the use of angle brackets such as `<organization>` and `<space>` in the previous command. 

If you don't know what your orginization and space are you can ommit them to login interactively:

    cf login -a https://api.ng.bluemix.net

Note: If you've just signed up your orginization is *probably* your e-mail address and your space is *probably* "dev"

#### Initialize the containers plugin

Run the follow command to initialize your IBM containers plugin:

    cf ic init
    
#### Set organization container namespace
Set your organization's namespace with the following commands. You may have set this already and if so this command will fail.

    cf ic namespace set <namespace>
    
#### Create a new space
Bluemix uses the concept of spaces to organize applications. Create and switch to a new space to hold the items created in this tutorial with the following commands.

    cf create-space tutorial
    cf target -s tutorial


### Deploy the First Discovery Server

The First Discovery Server includes the First Discovery Tool as a dependency so this step will take care of deploying both the First Discovery Tool *and* the First Discovery Server. These are referred to in the Overview of Components section as items 1 and 2.

#### Obtain the source

Obtain the source for the First Discovery Server:

    git clone https://github.com/GPII/first-discovery-server.git
    
    
#### Update the First Discovery Tool Version

Optionally, edit `package.json` from the `first-discovery-server` repository and edit the `"first-discovery"` dependency to a version of your choosing. 

In this tutorial we will be using this version:

     "first-discovery": "git+https://github.com/pga03/first-discovery.git#344530e2bed3653126d29e1e1763d089f2451f5b",

#### Build the image and push to Bluemix

Build the image and push it to Bluemix by running this command from the `first-discovery-server` folder: 

     cf ic build --rm=true --no-cache=true -t first_discovery_server .

Verify the image is listed in your registry:

    cf ic images
    
#### Create a container group

A container group in Bluemix is a cluster of containers, but in this tutorial we only create a single container
in the group. 

    cf ic group create \
    -p 8088 \
    --min 1 \
    --max 2 \
    --desired 1 \
    --memory 256 \
    --name first-discovery-group \
    -e NODE_ENV=bluemix \
    -e GPII_OAUTH2_AUTH_CLIENT_ID="net.gpii.prefsEditors.firstDiscovery" \
    -e GPII_OAUTH2_AUTH_CLIENT_SECRET="client_secret_firstDiscovery" \
    -e GPII_OAUTH2_HOST_NAME="<url for flow manager>" \      
    -e GPII_OAUTH2_TCP_PORT="80" \
    registry.ng.bluemix.net/<namespace>/first_discovery_server:latest                   # use your own namespace here
    
Note: These OAUTH2 secrets are taken from [test data](https://github.com/GPII/universal/blob/master/testData/security/TestOAuth2DataStore.js)

#### Monitor container group creation
    cf ic group list
Continue to the next step when the Status is `CREATE_COMPLETE`

#### Map a route to the container group
    cf ic route map --hostname firstdiscovery-<your initials> --domain mybluemix.net first-discovery-group
    
Note: If you recieve an error message of `{"message": "check domain error - failed to create domain, details: Invalid Auth Token"}` then run the command below and try to map the route again.

    cf ic init
    
#### Test the route
Open the route `http://firstdiscovery-<your initials>.mybluemix.net/demos/prefsServerIntegration` in your browser. 

Congratulations your site is now live!
