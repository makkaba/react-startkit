## set up

```
npm init -y

```

## install modules



``` sh
npm install --save react react-dom
```

``` sh
npm install webpack webpack-dev-server babel-core babel-loader babel-preset-es2015 babel-preset-react babel-preset-stage-2 --save-dev

```

## create static files

``` sh
mkdir src
touch src/index.html
```

```
<html>
    <head>
        <title>hello</title>

    </head>
    <body>
        
    </body>
</html>
```

## create configuration file for webpack

```
touch webpack.config.js
```

``` javascript
var webpack = require("webpack");
var path = require("path");

var DIST_DIR = path.resolve(__dirname, "dist");
var SRC_DIR = path.resolve(__dirname, "src");


var config = {
    entry: SRC_DIR + "/index.js",
    output: {
        path: DIST_DIR,
        filename: "bundle.js",
        publicPath: "/app/"
    },
    module: {
        loaders: [
            {
                test: /\?.js?/,
                include: SRC_DIR,
                loader: "babel-loader",
                query: {
                    presets: ["react", "es2015", "stage-2"]
                }
            }
        ]
    }
};

module.exports = config;
```

## add script reference in index.html

``` diff
<html>
    <head>
        <title>hello</title>

    </head>
    <body>
+       <script src="/app/bundle.js"></script>
    </body>
</html>
```

## create index.js

```sh
touch src/index.js

```

``` javascript
console.log("loaded!");
```

## add script to run

``` javascript
"scripts": {
    "start": "npm run build",
    "build": "webpack -d && cp src/index.html dist/index.html && webpack-dev-server --content-base src/ --inline --hot",
    "build:prod": "webpack -p && cp src/index.html dist/index.html"
  },
```

## let's run

```sh
npm start
```