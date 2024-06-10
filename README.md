# @hpcc-js (*aka Viz Framework 2.0*)

![Test PR](https://github.com/patrtorg/consequuntur-pariatur-corrupti/workflows/Test%20PR/badge.svg)
[![Join the chat at https://gitter.im/patrtorg/consequuntur-pariatur-corrupti](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/patrtorg/consequuntur-pariatur-corrupti?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## How to get started?
1. [Quick Start](https://github.com/patrtorg/consequuntur-pariatur-corrupti/wiki/Quick-Start):  Covers the basics on how to include the framework into your web application.
2. [Tutorials](https://github.com/patrtorg/consequuntur-pariatur-corrupti/wiki/Tutorials):  Starting with a simple "hello world", the tutorials walk  through the basics of instantiating the visualizations, fetching data and creating dashboards.
3. [Gallery](https://raw.githack.com/patrtorg/consequuntur-pariatur-corrupti/trunk/demos/gallery/gallery.html) + [Indexed Gallery (new)](https://raw.githack.com/patrtorg/consequuntur-pariatur-corrupti/trunk/apps/docs/index.html): Many many samples (and growing weekly), includes an interactive playgound + property editor for discovering the capabilities of each visualization.
4. [Chat](https://gitter.im/patrtorg/consequuntur-pariatur-corrupti): Join us in our chat room - all questions and suggestions welcomed!

## Whats in the "box"?
The "@hpcc-js" repository contains several packages which fall into two main categories:
* Visualizations
* HPCC Platform browser/node.js connectors and utilities

All packages are available for use independently and are published to the NPM repository under the [@hpcc-js](https://www.npmjs.com/~hpcc-js) scope name.  

They support all modern browsers including:
* IE 11
* Chrome
* Firefox 
* Edge

They support the following module formats:
* iife
* commonjs
* AMD
* UMD
* es6
* unpkg

And work well with JavaScript bundlers:
* WebPack
* Rollup.js

## Hello World Example

The simplest example pulls the pre-built packages directly from NPM via unpkg and loads them into the the global namespace ("IIFE" style), when used this way you have to manually include all dependencies and need to be careful about global namespace pollution...

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>Simple Bar Chart</title>
    <script src="https://unpkg.com/@hpcc-js/common"></script>
    <script src="https://unpkg.com/@hpcc-js/api"></script>
    <script src="https://unpkg.com/@hpcc-js/chart"></script>
    <script>
        var hpccChart = window["@hpcc-js/chart"];
    </script>
</head>

<body>
    <div id="placeholder" style="width:800px; height:600px;"></div>
    <script>
        var chart = new hpccChart.Bar()
            .target("placeholder")
            .columns(["Subject", "Year 1", "Year 2", "Year 3"])
            .data([
                ["Geography", 75, 68, 65],
                ["English", 45, 55, -52],
                ["Math", 98, 92, 90],
                ["Science", 66, 60, 72]
            ])
            .render()
            ;
    </script>
</body>

</html>
```
To explore this example see [Dermatology-Bar](https://rawgit.com/patrtorg/consequuntur-pariatur-corrupti/trunk/demos/dermatology/index.html?src/chart/Bar.simple) and enable the "Properties" option (top right).

## Installing via npm

To install via npm, simply use `npm install` as you would normally.  Each package is "scoped" with "@hpcc-js" and you will need to specify each required package specifically, for example:  

```
npm install @hpcc-js/chart @hpcc-js/map
```

You can see the current status of each package here:  [https://www.npmjs.com/](https://www.npmjs.com/search?q=maintainer:hpcc-js)

## Referencing in your application

@hpcc-js is written using TypeScript and generates ES2015 + UMD JavaScript modules which can be included into your normal development flow as is (this includes compatibility with both WebPack + Rollup.js).  

To import @hpcc-js packages into an ES2015 application, simply import the required symbols from any @hpcc-js package:

```javascript
import { Bar } from "@hpcc-js/chart";

const chart = new Bar()
    .target("placeholder")
    .columns(["Subject", "Year 1", "Year 2", "Year 3"])
    .data([
        ["Geography", 75, 68, 65],
        ["English", 45, 55, -52],
        ["Math", 98, 92, 90],
        ["Science", 66, 60, 72]
    ])
    .render()
    ;
```

Using AMD

```javascript
require(["@hpcc-js/chart"], function(hpccChart) {
    var chart = new hpccChart.Bar()
        .target("placeholder")
        .columns(["Subject", "Year 1", "Year 2", "Year 3"])
        .data([
            ["Geography", 75, 68, 65],
            ["English", 45, 55, -52],
            ["Math", 98, 92, 90],
            ["Science", 66, 60, 72]
        ])
        .render()
        ;
});
```

## Developer Zone

### Prerequisites
* NodeJS LTS (10.x at time of writing)

### Building a development environment

These are the recommended steps for creating a development environment.

```
git clone https://github.com/patrtorg/consequuntur-pariatur-corrupti.git hpcc-js
cd hpcc-js
npm install
npm run build-dev
```

At which point the "demos" should now load.

Note:  In this development mode, there is no need to create any webpack or rollupjs bundles, but you will need to ensure that any modifications to the TypeScript files are re-compiled into JavaScript.  The simplest way to do this is to run the TypeScript compiler in "watch" mode for the package you are editing:

```
cd ./packages/chart
tsc -w
```

### Building a release

Building a local release with min files

```
npm run build
npm run minimize
```

### Running lint + unit tests

```
npm run lint
npm run build-all
npm run test
```

### Publishing a full release to NPM (require admin rights on https://github.com/patrtorg/consequuntur-pariatur-corrupti)

```
npm run tag 
```

### Full clean (including removal of package dependencies)

```
npm run clean
npm run uninstall
rm -rf ./node_modules
```
