---
title: Start: FDT Local Environment Setup
layout: default
category: Tutorials
---

### Why do I need a First Discovery Tool Local Environment?

The main reason to have a local working environment for any project is so that you can actively make changes and see the results, without affecting anyone else's work. This will give you the ability to rapidly develop different aspects of the First Discovery Tool, while tracking your changes and providing merging capabilities. Additionally, you will need it for the majority of the tutorials on this site.

__Setup 1:__ Install Nodejs - https://nodejs.org/en/

__Setup 2:__ Install Github - https://desktop.github.com/ - This should include the command line version.
### 1. Clone first-discovery @ https://github.com/GPII/first-discovery
  * Open up Command Prompt
  * Navigate to your projects folder
  * RUN: __git clone https://github.com/GPII/first-discovery.git__
  
### 2. Clone first-discovery-server @ https://github.com/GPII/first-discovery-server
  * RUN: __git clone https://github.com/GPII/first-discovery-server.git__

![Command Prompt image showing two folders in the working directory](images/localEnvironment1.png)

### 3. Install first-discovery-server
  * RUN: __cd first-discovery-server__
  * RUN: __npm install__ - Ignore the errors
  * Navigate to src/config/environment.json
  * Delete the code and change it to the following:

__environment.json__
```json
{
    "type": "firstDiscovery.server.environment.config",
    "options": {
        "gradeNames": ["gpii.firstDiscovery.server.configurator"],
        "port": "8088",
        "preferencesConfig": {
            "securityServer": {
                "port": "{gpii.resolvers.env}.vars.GPII_OAUTH2_TCP_PORT",
                "hostname": "{gpii.resolvers.env}.vars.GPII_OAUTH2_HOST_NAME",
                "paths": {
                    "token": "{gpii.resolvers.env}.vars.GPII_OAUTH2_ACCESS_TOKEN_PATH",
                    "preferences": "{gpii.resolvers.env}.vars.GPII_OAUTH2_ADD_PREFERENCES_PATH"
                }
            },
            "authentication": {
                "grant_type": "{gpii.resolvers.env}.vars.GPII_OAUTH2_AUTH_GRANT_TYPE",
                "scope": "{gpii.resolvers.env}.vars.GPII_OAUTH2_AUTH_SCOPE",
                "client_id": "testing",
                "client_secret": "No Secret"
            }
        }
    },
    "require": ["../js/firstDiscoveryServer.js"]
}
```

### 4. Navigate to ../first-discovery-server/node_modules
  * RUN: __cd node_modules__
  * RUN: __dir__ - to see the contents of node modules

### 5. Locate and delete gpii-first-discovery
  * RUN: __RD /S gpii-first-discovery__
  * Yes, Delete the folder
  
![Command Prompt image showing deletion process for the gpii-first-discovery folder](images/localEnvironment2.png)

### 6. Get the path to your first-discovery clone
  * Open Windows Explorer
  * Navigate into your first-discovery clone
  * Click the folder icon in the top left to reveal the path
  * Right click and copy the path.
  
![Windows Explorer image showing how to get the path to the first discovery clone](images/localEnvironment3.png)  
  
### 7. Create a Symlink in the node_modules folder of the first-discovery-server named gpii-first-discovery linking to the first-discovery clone.
  * Right-Click Command Prompt and select "Run as Adminstrator"
  * Navigate back to ../first-discovery-server/node_modules 
  * RUN: __mklink /D gpii-first-discovery "C:\Users\IBM_ADMIN\Desktop\FDT Setup Example\first-discovery"__
  * RUN: __dir__ - make sure the folder* is there.
  
![Command Prompt image showing that the symlink has been created](images/localEnvironment4.png)  

![Command Prompt image showing Symlink in the directory](images/localEnvironment5.png)  
    
### 8. Navigate back to the ../first-discovery-server
  * RUN: __cd ..__

### 9. Run: node index.js (this starts the first-discovery local server)
  * RUN: __node index.js__

### 10. Open Google Chrome and navigate to -> http://localhost:8088/demos/prefsServerIntegration/index.html?preview=electron