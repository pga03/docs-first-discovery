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


## Overview of steps
1. Login  
2. Set up tools
3. Build image
4. Deploy container group
5. Test

## Procedure

1. Login  
    A. Run the following command to login. Note: command text with `<variables>` should be substituted for your own values. If you've just signed up your orginization is *probably* your e-mail address and your space is *probably* "dev"
    
        cf login -a https://api.ng.bluemix.net -o <orginization -s <space>
        
    B. If you don't know what your orginization and space are you can ommit them to login interactively:      
    
        cf login -a https://api.ng.bluemix.net
  
2. Set up tools

    A. Run the follow command to initialize your IBM containers plugin:

        cf ic init
    
    B. Set your organization's namespace with the following commands. You may have set this already and if so this command will fail.

        cf ic namespace set <namespace>
    
    C. Create and switch to a new space to hold the items created in this tutorial with the following commands.

        cf create-space tutorial
        cf target -s tutorial

3. Build image  
    A. Obtain the source for the First Discovery Server:

        git clone https://github.com/GPII/first-discovery-server.git    
    
    B. Optionally, edit `package.json` from the `first-discovery-server` repository and edit the `"first-discovery"` dependency to a version of your choosing. In this tutorial we will be using version 
        
        git+https://github.com/pga03/first-discovery.git#344530e2bed3653126d29e1e1763d089f2451f5b
    
    C. Build the image and push it to Bluemix by running this command from the `first-discovery-server` folder: 

        cf ic build --rm=true --no-cache=true -t first_discovery_server .
        
    D. Verify the image is listed in your registry:

        cf ic images
    
4. Deploy container group  
    A. Create a container group, which is like a cluster of containers, with the following command.  Note: These OAUTH2 secrets are taken from [test data](https://github.com/GPII/universal/blob/master/testData/security/TestOAuth2DataStore.js)

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

    B. Monitor container group creation until the status is `CREATE_COMPLETE`
    
        cf ic group list

    C. Map a route to the container group
    
        cf ic route map --hostname firstdiscovery-<your initials> --domain mybluemix.net first-discovery-group
    
    D. If you recieve an error message of `{"message": "check domain error - failed to create domain, details: Invalid Auth Token"}` then run the command below and try to map the route again.

        cf ic init
    
5. Test

    A. Open the route `http://firstdiscovery-<your initials>.mybluemix.net/demos/prefsServerIntegration` in your browser. 

Congratulations your site is now live!
