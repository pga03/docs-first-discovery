# First Discovery Tool Documentation

This project contains the content needed to build and deploy the First Discovery Tool Documentation. It is based off of the Fluid `docs-template` project.

# To Build

1. Clone this repository.
2. From within the project's directory, install DocPad if it isn't already installed: `sudo npm install -g docpad`
3. Get the required node modules: `npm install`
4. Run docpad: `docpad run`
5. Confirm everything is working by loading `http://localhost:9778/` in a web browser.

# Getting Updates from docs-template for the First Discovery Tool Documentation

Periodically `docs-template` will have updates. It is suggested you keep up to date with these changes:

```
git remote add docs-template  https://github.com/fluid-project/docs-template
git fetch docs-template
git merge docs-template/master
npm update
```

Conflicts may occur when merging in changes from `docs-template` to your custom site. Manually resolve each conflict.

# Deploy to GitHub Pages
```
docpad deploy-ghpages --env static
```

*Note:* The above command will deploy to the origin of the repository. To deploy to production, you may need to be working from Master, not a fork.

# Generating a static version
To create a static version of the site, run: `docpad generate --env static`. This will generate a version in the `./out/` directory which you can then view locally or upload to a web server.
