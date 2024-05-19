# Quasar Inputs

Welcome to Quasar Inputs demo!

## Introduction

This repository hosts a demonstration of handling input validation for number-only fields using HTML `input type="number"` attribute and Quasar's `keyup` and `keydown` events.

[See it in action](https://divensky.github.io/quasar-inputs/#/).

## Purpose

The purpose of this demo is to showcase how browsers handle non-numeric inputs in number-only fields. It provides a practical example of custom validation using Quasar's events.

## Features

* Demonstrates how browsers interpret non-numeric inputs in number-only fields.
* Highlights the [limitations](https://bugzilla.mozilla.org/show_bug.cgi?id=1855719) of traditional validation methods for such inputs.
* Provides a hands-on demonstration of custom validation using Quasar's events.

## Usage

[Open the demo](https://divensky.github.io/quasar-inputs/#/).

Or clone/download this repo and run:

```bash
npm run dev
```

## Feedback

Feedback is welcome! Please star the repo if you liked it.

If you encounter any issues or have suggestions for improvements, please feel free to open an issue or submit a pull request.

---

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

If this is a Vite app (not a Quasar app) then the file to change the settings is `vite.config.ts` and you want to include a line `base: "/repo-name/"`, for example:
```
export default defineConfig({
  base: "/my-repo-example/",  
});
```

Additionally, in this case you need to update the Vue router settings with the correct path, for example:

```
const router = createRouter({
  history: createWebHistory('/my-repo-example/'),
});
```

2. Run the command: `npm run build`

It runs `quasar build` in Vite. This command generates a `/dist/spa` directory containing the built files.

Make sure it generated the correct path. Opened the generated `index.html` file and look for asset paths in its `head`. The correct ones should include the user name and repo name like this: `https://divensky.github.io/my-repo/assets/index.ef5b4270.js`.

3. Switch to a branch dedicated to GitHub Pages deployment, let's call it `gh-pages`:

```
git checkout -b gh-pages
```

4. In this branch delete the unnecessary files. The important thing to delete is `index.html` file so it will not conflict with the files you're going to copy over and use.

You might wish to delete all other files so they don't clutter the space.

You can keep the ReadMe file in the root and delete all of the configs. I've kept the `.gitignore` file and `node_modules` folder (if you delete it, it's gone from the `main` branch as well and you have to `npm install` it again). I deleted the `src` folder.

5. Copy the entire contents (files and subfolders) of the `/dist/spa` directory to the root of the deployment branch `gh-pages`.

This can be done in a file explorer by Ctrl+C Ctrl+V, or it can be done on the command line.

6. Commit the changes to the `gh-pages` branch and push them to GitHub. You can do this using Git commands:

```
git add .
git commit -m "Deploy Quasar app to GitHub Pages"
git push origin gh-pages
```

7. Configure the GitHub Pages: Go to the repository on GitHub, click on the "Settings" tab, scroll down to the "Pages" section in the left menu and open "GitHub Pages" page.

Under "branch", select your branch name (`gh-pages` in the above example) as the source. This tells GitHub Pages to serve the content from your selected branch.

8. Be patient for a few minutes to allow the deployment to propagate. Then access your content at `https://<username>.github.io/<repo>/`.

9. Debug in case of errors:

- Make sure you're serving a static page: the above steps will not work for server-side functionality like databases or user authentication without additional setup.
- Open the Browser's Developer Tools and check the console for errors. Inspect the Network Tab: look for any failed requests (highlighted in red) and see the paths to the app's assets and compare them to what you have.
- Make sure that the structure of the files in your `gh-pages` branch matches the structure of the /dist/spa directory after building your Quasar app. The `index.html` file should be at the root, and all other assets (CSS, JavaScript, images) should be in their correct subdirectories.

10. Update the served page whenever needed:

- In your main branch (the branch that has your updates) newly run `npm run build` to generate the updated build files.

- Copy the contents of the `/dist/spa` directory from this branch into a temp folder. You want to be able to access these files from any branch.

- Switch to the deployment branch (`gh-pages` in the above example). Delete old deploy files and any unncecessary files as above.

- Copy all deploy files from the temp folder to this directory.

- Commit and Push:

```
git add .
git commit -m "Update Quasar app on GitHub Pages"
git push
```

- You might wait a few minutes for the updates to propagate and/or reload your browser window (Ctrl + F5) to see the updated version on your page.




