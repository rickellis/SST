# How to install Svelte with Snowpack and Tailwind.

This document describes how to set up [Svelte](https://svelte.dev) with [Snowpack](https://www.snowpack.dev) and [Tailwind CSS](https://tailwindcss.com).


### Install Snowpack

```shell
npx create-snowpack-app PROJECT-NAME --template @snowpack/app-template-minimal

cd PROJECT-NAME

// Run Snowpack to make sure it's working
npm run start
```

### Install Svelte and Tailwind

```shell
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
// Add the plugin array
'@snowpack/plugin-svelte',
'@snowpack/plugin-postcss'

// Add this to mount array:
public: '/',
src: '/dist',

// To build using ESBuild, add the experiments object:
// https://esbuild.github.io
  "experiments": {
    "optimize": {
      "bundle": true,
      "minify": true,
      "target": 'es2018'
    }
  }
```

Create two new folders:

```html
src
public
```

Move `index.css` and `index.html` into `public`:

```html
public
    index.css
    index.html
```

Move `index.js` into `src` and create a new file called `App.svelte` in there as well:

```html
src
    App.svelte
    index.js
```


Replace the contents of `public/index.html` with:

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

Replace the contents of `public/index.css` with:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```


Replace the contents of `src/index.js` with:

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

Replace the contents of `src/App.svelte` with:

```html
<!-- App.svelte -->
<script></script>
<style></style>
<div class="px-5 bg-green-300 box">
    <p>Hello world!</p>
</div>
```

Create a file called `postcss.config.js` in the root and add this:

```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  }
}
```

Add this to the purge[] array in `tailwind.config.js`

```js
'./src/**/*.html',
'./src/**/*.js',
'./src/**/*.svelte',
```