# Quasar Inputs

Welcome to Quasar Inputs!

## Overview

Currently this app displays a Number input with custom validation.

[See it in action](https://divensky.github.io/quasar-inputs/#/).

## How to run in dev mode

```bash
quasar dev
```

## How to deploy a static Vue app on a GitHub page

The following steps were taken to create a page for this app and can be followed for other similar apps:

1. In `quasar.config.js` change the `pubicPath` to include your repo name. This assumes you want to deploy to a page corresponding to your repo name. For example, in this repo this is: https://divensky.github.io/quasar-inputs/

```
// quasar.config.js
module.exports = function (/* context */) {
 return {
    // ...
    build: {
      // ...
      publicPath: '/<repo>/',
    },
 };
};
```

Example:

```
     publicPath: '/quasar-inputs/',
```

2. Run the command: `npm run build`

It runs `quasar build` in Vite. This command generates a `/dist/spa` directory containing the built files.

3. Create a new branch (let's say `gh-pages`) and switch to it in the IDE or in the terminal:

```
git checkout -b gh-pages
```

4. In this new branch delete the unnecessary files. The important thing to delete is `index.html` file so it will not conflict with the files you're going to copy over and use.

You might delete all other files so they don't clutter the branch. I deleted the `src` folder for example.

You can keep the ReadMe file in the root and delete all of the configs. I've kept the `.gitignore` file and `node_modules` folder (if you delete it, it's gone from the `main` branch as well and you have to `npm install` it again).

5. Copy the entire contents of the `/dist/spa` directory to the root of this deployment branch (we call it `gh-pages`). This would include its files and subfolders.

This can be done in a file explorer by Ctrl+C Ctrl+V, or it can be done on the command line.

6. Commit the changes to your `gh-pages` branch and push them to GitHub. You can do this using Git commands:

```
git add .
git commit -m "Deploy Quasar app to GitHub Pages"
git push origin gh-pages
```

7. Configure the GitHub Pages: Go to the repository on GitHub, click on the "Settings" tab, scroll down to the "Pages" section in the left menu and open "GitHub Pages" page.

Under "branch", select your branch name (`gh-pages` in the above example) as the source. This tells GitHub Pages to serve the content from your selected branch.

8. Access the Quasar App: After configuring GitHub Pages, this Quasar app should be accessible at `https://<username>.github.io/<repo>/`.

It might take a few minutes for the deployment to propagate.

9. Debug in case of errors:

- Make sure you're serving a static page: the above steps will not work for server-side functionality like databases or user authentication without additional setup.
- Open the Browser's Developer Tools and check the console for errors. Inspect the Network Tab: look for any failed requests (highlighted in red) and see the paths to the app's assets and compare them to what you have.
- Make sure that the structure of the files in your gh-pages branch matches the structure of the /dist/spa directory after building your Quasar app. The index.html file should be at the root, and all other assets (CSS, JavaScript, images) should be in their correct subdirectories.

10. Update the served page whenever needed:

- In your main branch (the branch that has your updates) newly run `npm run build` to generate the updated build files.

- Copy the contents of the `/dist/spa` directory from this branch into a temp folder. You want to be able to access these files from any branch.

- Switch to the deploy branch (`gh-pages` in the above example). Delete old deploy files and any unncecessary files as above.

- Copy all deploy files from the temp folder to this directory.

- Commit and Push:

```
git add .
git commit -m "Update Quasar app on GitHub Pages"
git push
```

- You might wait a few minutes for the updates to propagate and/or reload your browser window (Ctrl + F5) to see the updated version on your page.




