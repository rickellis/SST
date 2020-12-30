# SST - Svelte, Snowpack, and Tailwind.

This document describes how to set up a Svelte installation that uses Snowpack instead of a traditional bundler. It also uses Tailwind CSS.


### Install Snowpack

```js
    npx create-snowpack-app PROJECT-NAME --template @snowpack/app-template-minimal

    cd PROJECT-NAME

    // Run Snowpack to make sure it's working
    npm run start
```

### Install Svelte and Tailwind

```js
    npm install svelte --save

    npm install tailwindcss@latest postcss@latest autoprefixer@latest
    npx tailwindcss init

    // These are Snowpack plugins for Svelte and Tailwind
    npm install @snowpack/plugin-svelte --save-dev
    npm install --save-dev @snowpack/plugin-postcss postcss postcss-cli
```

### Update the Snowpack config file

Add these items to `snowpack.config.js`

```js
    // Add the plugin to your snowpack.config.js file
    '@snowpack/plugin-svelte',
    '@snowpack/plugin-postcss'

    // Add this to mount:
    public: '/',
    src: '/dist',

  // To build using ESBuild, add the experimental feature
  // https://esbuild.github.io
    "experiments": {
      "optimize": {
        "bundle": true,
        "minify": true,
        "target": 'es2018'
      }
    }
```


Create two folders and move/create the files:

```html
src
    App.svelte
    index.js
public
    styles.css
    index.html
```

Here's the contents of `index.js`

```js
// index.js
import App from "./App.svelte";

let app = new App({
  target: document.body,
});

export default app;

// Hot Module Replacement (HMR) - Remove this snippet to remove HMR.
// Learn more: https://www.snowpack.dev/concepts/hot-module-replacement
if (import.meta.hot) {
    import.meta.hot.accept();
    import.meta.hot.dispose(() => {
      app.$destroy();
    });
  }
```

Here's the contents of `App.svelte`

```js
<!-- App.svelte -->
<script>
 
</script>
<style>

</style>
<div class="px-5 bg-green-300 box">
    <p>Hello world!</p>
</div>
```

Here's the contents of `index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="stylesheet" type="text/css" href="./styles.css" />
    <title>SITE NAME</title>
  </head>
  <body>
    <script type="module" src="./dist/index.js"></script>
  </body>
</html>
```

Here's the contents of `publid/styles.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Create a file called `postcss.config.js` and add this:

```js
module.exports = {
    plugins: {
      tailwindcss: {},
      autoprefixer: {},
    }
  }
```
