# SST
Svelte using Snowpack and Tailwind

This document describes how to set up a Svelte installation that uses Snowpack instead of a traditional bundler, along with Tailwind CSS.

The above tools, in my view represent the future of web development. I'm an old-school web developer. I got online in 1996 and cut my teeth in the early, renegade days of the internet. Around 2010 I took a decade long break from writing code. When I came back to development I was shocked by the insane levels of complexity required to be a front end developer today. To be in the game now, you had to be an expert in Node, frameworkds, bundlers, language extensions, and a myriad of other tools. As someone that has always valued simplicity, clarity, and modularity this felt like lugging around a 1000 pound gorilla just to make a simple website.

There has to be a better way. Well, there is. Thanks to browsers now supporting module imports natively, and thanks to brilliant minds that dared to buck the status quo and think about what modern web development should be.

[Svelte](https://svelte.dev) is an alternative to Javascript frameworkds like React or Vue, one that uses a completely different paradigm: Compilation. Instead of your browser doing all the work required to run a framework, it buids your code as plain vainilla Javascript using a compiler. No more virtual DOMs or bloated tooling. The compile builds only what you need for your app in native JS. This results in drastically, measurably faster code. Plus, with Svelte you write drastically less code than what you'd use with a typical framework. Plus, the paradigm with Svelte is reversed: Whereas with othe frameworkds, you write Javascirpt files that contain HTML, in Svelte you write HTML files that contain Javascirpt. 

[Snowpack](https://www.snowpack.dev) is a lightning-fast frontend build tool that leverages JavaScript's native module system (known as ESM). Bundlers such as Webpack or Rollup were needed to solve a critical problem for web developers: No native browser support for module imports. That's no longer an issue. Snowpack is a modern approach to bundling that is much faster and efficient for development. 

[Tailwind](https://tailwindcss.com) is a CSS framework that lets you mostly never have to touch a CSS file.  Adam Wathan, the creator of Tailwind, has a [great article](https://adamwathan.me/css-utility-classes-and-separation-of-concerns/) that describes the how and why of Tailwind.

