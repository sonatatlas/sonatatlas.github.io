---
layout: post
title: Compiler Typescript in Webpack
categories: react
---

# Steps

+ Adding TypeScript compiler(tsc) to your build pipeline.
+ Converting JavaScript files into TypeScript files.

# Understand the existing JavaScript project

Webpack as bundler & task runner, and `babel-loader` Webpack plugin to use Babel for ES6 and JSX transpilation. 

```
TicTacToe_JS /
    |---- css/			        // css style sheets
    |---- src/			        // source files
        |---- app.jsx		        // the App React component
        |---- board.jsx		        // the TicTacToe Board React component
        |---- constants.js		// some shared constants
        |---- gameStateBar.jsx	        // GameStatusBar React component
        |---- restartBtn.jsx	        // RestartBtn React component
    |---- .babelrc		        // a list of babel presets
    |---- index.html		        // web page for our app
    |---- package.json		        // node package configuration file
    |---- webpack.config.js	        // Webpack configuration file
    
```

# Add TypeScript compiler to build pipeline

## install dependencies

`awesome-typescript-loader` is a Webpack plugin that helps you compile TypeScript code to JavaScript, much like babel-loader for Babel.

```
yarn add -D typescript awesome-typescript-loader source-map-loader
```

Get the type declaration files (.d.ts files) from @types for any library in use. For this project, we have React and ReactDOM.

```
yarn add -D @types/react @types/react-dom
```


# Configure TypeScript

Next, configure TypeScript by creating a `tsconfig.json` file in src, and add,

```
"compilerOptions": {
    "outDir": "./dist/",  // path to output directory
    "sourceMap": true,  // allow sourcemap support
    "strictNullChecks": true,  // enable strict null checks as a best practive
    "module": "es6",  // specify module code generation
    "jsx": "react",  // use typescript to transpile jsx to js
    "target": "es5",  // specify ECMAScript target version
    "allowJs": true  // allow a partial TypeScript and JavaScript codebase
},
"include": [
    "./src/"
]
```

# Set up build pipeline

modify `webpack.configure.js` as below,

```
  // change to .tsx if necessary
  entry: './src/app.jsx',
  output: {
    filename: './dist/bundle.js'
  },
  resolve: {
    // changed from extensions: [".js", ".jsx"]
    extensions: [".ts", ".tsx", ".js", ".jsx"]
  },
  module: {
    rules: [
      // changed from { test: /\.jsx?$/, use: { loader: 'babel-loader' } },
      { test: /\.(t|j)sx?$/, use: { loader: 'awesome-typescript-loader' } },
      // addition - add source-map support
      { enforce: "pre", test: /\.js$/, loader: "source-map-loader" }
    ]
  },
  externals: {
    "react": "React",
    "react-dom": "ReactDOM",
  },
  // addition - add source-map support
  devtool: "source-map"

```
