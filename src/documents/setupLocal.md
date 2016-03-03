---
title: Start: First Discovery Local Environment Setup
layout: default
category: Tutorials
---

### Why do I need a First discovery Local Environment?

The main reason to have a local working environment for any project is so that you can actively make changes and see the results, without affecting anyone else's work. This will give you the ability to rapidly develop different aspects of the First Discovery Tool, while tracking your changes and providing merging capabilities. Additionally, you will need it for the majority of the tutorials on this site.

### 1. Clone first-discovery

### 2. Clone first-discovery-server

### 3. Install first-discovery-server

### 4. Navigate to ../first-discovery-server/node_modules

### 5. Locate and delete gpii-first-discovery

### 6. Get the path to your first-discovery clone

### 7. Create a Symlink in the node_modules folder of the first-discovery-server named gpii-first-discovery linking to the first-discovery clone.

### 8. Navigate back to the ../first-discovery-server

### 9. Run: node index.js (this starts the first-discovery local server)

### 10. Open Google Chrome and navigate to -> http://localhost:8088/demos/prefsServerIntegration/index.html?preview=electron

## Recommended Workflow Example

### 1. Start up first-discovery-server with node index.js

### 2. Open up first-discovery on your ide of choice

### 3. Open up command line/prompt, navigate to ../first-discovery and switch to a new branch

### 4. Open up Google Chrome and check your work @ http://localhost:8088/demos/prefsServerIntegration/index.html?preview=electron

### 5. Repeat the following

  * Make changes to first-discovery
  * Refresh Google Chrome to see the results.

### 6. Push & Commit to github

### 7. Perform a Merge Request

### 8. Handle any Merge Conflicts

### 9. Delete your branch (unless there is a reason to keep it)
