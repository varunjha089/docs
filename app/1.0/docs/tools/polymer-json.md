---
title: polymer.json
---

Adding a top-level `polymer.json` file to your project allows you to describe and configure different settings for your Polymer application. Below is a list of all supported options you can use.

## Supported Properties

### `entrypoint`

The main entrypoint into your application for all routes, defaults to your `index.html` file if one is found. This file should import the app shell file specified by the "shell" option. It should be minimal since it's loaded and cached for every route.

```json
{
  "entrypoint": "index.html"
}
```


### `shell`

The app shell file containing common code for the app.

```json
{
  "entrypoint": "index.html",
  "shell": "src/app-shell/app-shell.html"
}
```

### `fragments`

An array of any HTML files that are not synchronously loaded from the app shell, such as async imports or any imports loaded on-demand (e.g. by importHref).

```json
{
  "entrypoint": "index.html",
  "shell": "src/app-shell/app-shell.html",
  "fragments": [
    "src/view-one/view-one.html",
    "src/view-one/view-two.html"
  ]
}
```


### `sources`

An array of globs matching your application source files. This will default to all files in your project `src/` directory, but configuring your own list of sources can be useful when your source files live in other directories.

```json
{
  "entrypoint": "index.html",
  "shell": "src/app-shell/app-shell.html",
  "fragments": [
    "src/view-one/view-one.html",
    "src/view-one/view-two.html"
  ],
  "sources": [
    "src/**/*",
    "images/**/*",
    "bower.json"
  ]
}
```


### `includeDependencies`

An optional array of globs matching any additional dependencies you'd like to include with your build. If your application loads any files dynamically they can be missed by the analyzer, but you can include them here to make sure that they are always added to your build.

```json
{
  "entrypoint": "index.html",
  "includeDependencies": [
    "bower_components/webcomponentsjs/webcomponents-lite.min.js"
  ]
}
```


### `builds`

```json
{
  "entrypoint": "index.html",
  builds: [{
    "addServiceWorker": true,
    "js": {"minify": true},
    "css": {"minify": true},
    "html": {"minify": true}
  }]
}
```