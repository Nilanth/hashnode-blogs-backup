## Use Vite for React Apps instead of CRA

Most of us will be using [Create React App](https://create-react-app.dev/) for creating [React](https://reactjs.org/) App. It supports all the configurations out of the box. But when your project code grows you might face higher build times, a slower start in the development server and waiting 2 to 5 secs to reflect the changes you have made in code and this might increase rapidly when the app grows on a larger scale.

This increases

1. Development time, as we need to wait for 2 to 6 secs for each change.
2. Production Build Time, it might take around 10 to 20 minutes to deploy a quick fix.
3. Time, Time is money 🙂.

## Why CRA dev server is slow?

CRA uses [Webpack](https://webpack.js.org/) to bundle the code. Webpack bundles the entire code, so if your codebase is very large more than 10k lines you might see a slower start in the development server and a long waiting time to see the changes made.

![bundler-image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/x88w1bkng42yg8iyzlz2.png)

As you can see in the above image, the Entire code is bundled to make the server ready for development.

## How to make it faster?

Instead of using CRA for creating React App, we can migrate to [Vite](https://vitejs.dev/). Vite is the next generation frontend tooling to build the app faster.

## Highlights of Vite

1. On-demand file serving over native ESM, no bundling required!
2. Hot Module Replacement (HMR) that stays fast regardless of app size.
3. Out-of-the-box support for TypeScript, JSX, CSS and more.
4. Pre-configured Rollup builds with multi-page and library mode support.
5. Rollup-superset plugin interface shared between dev and build.
6. Flexible programmatic APIs with full TypeScript typing.
7. Supports React, [Vue](https://vite.new/vue), [Preact](https://vite.new/preact), [Svelte](https://vite.new/svelte).

## How Vite is faster than CRA?

Vite uses [esbuild](https://esbuild.github.io/) which is written in Go and pre-bundles dependencies **10–100x faster** than JavaScript-based bundlers.

Vite improves the development server start time by dividing the modules of an application into two categories: **dependencies** and **source code**.

**Dependencies** are mostly plain JavaScript that does not change often during development. Some large dependencies (e.g. [AntD](https://ant.design/)) are also quite expensive to process.

**Source code** often contains non-plain JavaScript that needs transforming (e.g. JSX, CSS or etc components), and will be edited very often. Also, not all source code needs to be loaded at the same time (e.g. with route-based code-splitting).

![vite-build](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/y1ii4q0ss46cyoi1sbt8.png)

As you see in the above image, Vite only needs to transform and serve source code on demand, when the browser requests it. Code-behind conditional dynamic imports are only processed if actually used on the current screen.

I have migrated an existing CRA based react app to Vite. Let’s compare the difference.

## CRA Dev server start duration

![cra-dev-server](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mtcgbgawtelob5f2597y.png)

**CRA** took **12s** to start the development server. The sample app only contains 2 routes and 6 components. Let’s see the same using Vite

## Vite Dev server start duration

![vite-dev-server](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/igjpnjfb73byv62igdj2.png)

**Vite** only took **298ms** to start the dev server, It’s blazing fast when compared to CRA. As you can see a huge difference between the two tools. Let’s also compare the production build time of both.

## CRA build duration

![cra-build](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hpxjtscofh7qsc9bqftg.png)

CRA took **16.66s** to build the app. Let’s see Vite's performance.

## Vite build duration

Vite uses the **same bundle approach** for production build with [Rollup](https://rollupjs.org/guide/en/), as using unbundled native ESM in production will cause extra HTTP requests.

![vite-build](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uws35q2wjits6nk3f6rq.png)

Vite with rollup took only **9.11s** to build the entire app, Seems better compared to CRA. As it reduces the 40 to 50 percentage for build time when using Vite. This is more effective. For instance, if your current build time is 20 minutes, it will come down to 10 to 12 minutes when using Vite 🚀.

> Not satisfied with the comparison check this [tweet](https://twitter.com/amasad/status/1355379680275128321).

Hope you are thinking about how to **migrate your current React CRA app to Vite**?

It’s not a big deal! Let start over

## Migration CRA to Vite

- Remove the **react-scripts** from the **package.json** dependency.
- Add sass in **package.json**, if you are using CSS or SCSS.
- Add the below dependencies as a dev dependency
```
"devDependencies": {
  "@vitejs/plugin-react": "1.1.1",
  "vite": "2.7.0"
},
```
- Add the below commands to scripts
```
"scripts": {
  "start": "vite",
  "build": "vite build"
},
```
- Create a file **vite.config.js** in the root folder and add the below code

%[https://gist.github.com/Nilanth/dc7cfeb9bb2a24f9de78d2bf1a27c44e]


**react()** is used to avoid the manual import of `React` in `.jsx` and `.tsx` modules.

- Move the **index.html** file outside public the folder.

- Remove all the `%PUBLIC_URL%` from `index.html`

```
//From
<link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
//To
<link rel="icon" href="/favicon.ico" />
```
- Add the below script tag in the body of the **index.html**

```
<div id="root"></div>
<script type="module" src="/src/index.jsx"></script> // Need to add
```
- Update your ENVs from **REACT_APP** to **VITE** as below

```
// From
REACT_APP_ENV = local
REACT_APP_HOST_UR = https://reqres.in/api/
// To
VITE_ENV = local
VITE_HOST_URL = https://reqres.in/api/
```
- Now just run **npm install** or **yarn**

- Now run **yarn start** or **npm start**, Done!. Now our CRA app is migrated to Vite.

## Notes:

If you face any issues in importing the components use the [resolve alias](https://vitejs.dev/config/#resolve-alias).

## New React App using Vite

Use the below command to create a fresh react app.

```
yarn create vite my-react-app --template react
```

## Reference

2. [Vite](https://vitejs.dev/)
3. [esbuild](https://esbuild.github.io/)
4. [Rollup](https://rollupjs.org/guide/en/)
5. [Vite preset templates](https://github.com/vitejs/vite/tree/main/packages/create-vite)

## Conclusion
Vite seems very efficient, speeder and saves more time compared to CRA. Try **Vite**, you can see the difference.

Thank you for reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).