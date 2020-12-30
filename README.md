# SST - Svelte, Snowpack, and Tailwind.

Svelte using Snowpack and Tailwind

This document describes how to set up a Svelte installation that uses Snowpack instead of a traditional bundler, along with Tailwind CSS.

[Svelte](https://svelte.dev) is an alternative to Javascript frameworkds like React or Vue, one that uses a completely different paradigm: Compilation. Instead of your browser doing all the work required to run a framework, it buids your code as plain vainilla Javascript using a compiler. No more virtual DOMs or bloated tooling. The compile builds only what you need for your app in native JS. This results in drastically, measurably faster code. Plus, with Svelte you write drastically less code than what you'd use with a typical framework. Plus, the paradigm with Svelte is reversed: Whereas with othe frameworkds, you write Javascirpt files that contain HTML, in Svelte you write HTML files that contain Javascirpt. 

[Snowpack](https://www.snowpack.dev) is a lightning-fast frontend build tool that leverages JavaScript's native module system (known as ESM). Bundlers such as Webpack or Rollup were needed to solve a critical problem for web developers: No native browser support for module imports. That's no longer an issue. Snowpack is a modern approach to bundling that is much faster and efficient for development. 

[Tailwind](https://tailwindcss.com) is a CSS framework that lets you mostly never have to touch a CSS file.  Adam Wathan, the creator of Tailwind, has a [great article](https://adamwathan.me/css-utility-classes-and-separation-of-concerns/) that describes the how and why of Tailwind.


```js
    npx create-snowpack-app PROJECT-NAME --template @snowpack/app-template-minimal

    cd PROJECT-NAME
    npm run start

    npm install svelte --save
    npm install @snowpack/plugin-svelte --save-dev


    // Add the plugin to your snowpack.config.js file

    '@snowpack/plugin-svelte'    

    // In the same file, add this to mount

    public: '/',
    src: '/dist',

  // And add the experimental bundling:
    "experiments": {
      "optimize": {
        "bundle": true,
        "minify": true,
        "target": 'es2018'
      }
    }
```


Create two folders and move/create the files:

```js
src
    App.svelete
    index.js
public
    index.css
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
    <link rel="stylesheet" type="text/css" href="./index.css" />
    <title>SITE NAME</title>
  </head>
  <body>
    <script type="module" src="./dist/index.js"></script>
  </body>
</html>
```



## Install Tailwind

```js
    npm install tailwindcss@latest postcss@latest autoprefixer@latest
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

Initialize Tailwind:

```js
npx tailwindcss init
```

Add the tailwind css to `public/index.css`

```css
/* ./your-css-folder/styles.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Add the postCSS plugin to your install

```js
    npm install --save-dev @snowpack/plugin-postcss postcss postcss-cli

    // In your snowpack.config.js file add this plugin:

     '@snowpack/plugin-postcss'

```