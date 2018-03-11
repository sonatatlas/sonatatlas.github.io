---
layout: post
categories: react
title: Startup React Native App with Typescript
---

- [github][udtrokia]
- [ts-jest][jest]
- [typescript][ts]

_

## Run ts and tsx with ts-jest
 
# babel-jest
 
install
```
yarn add -D babel-jest babel-preset-react-native
```

# babelrc
Ensure `.babelrc` contains:

```json
{
    "presets": ["react-native"],
    "sourceMaps": "inline"
}
```

# transform
In `package.json`, inside jest section, `transform`:
```json
"transform":{
    "^.+\\.jsx?$": "<rootDir>/node_modules/babel-jest",
    "^.+\\.tsx?$": "ts-jest"
}
```

# fully completed jest

```json
    "preset": "react-native",
    "transform": {
      "^.+\\.jsx?$": "<rootDir>/node_modules/babel-jest",
      "^.+\\.tsx?$": "ts-jest"
    },
    "testRegex": "(/__tests__/.*|(\\.|/)(test|spec))\\.(jsx?|tsx?)$",
    "moduleFileExtensions": [
      "ts",
      "tsx",
      "js",
      "jsx",
      "json",
      "node"
    ],
    "globals": {
      "ts-jest": {
        "useBabelrc": true
      }
    }
```

## Introducing TypeScript

first, create `tsconfig.json`
```shell
tsc --init --pretty --sourceMap --target es2015 --outDir ./lib --module commonjs --jsx react
```
second, add `./src` to the `"include"` section of our tsconfig.json

```json
{
    "compilerOptions": {
        // other options here
    },
    "include": ["./src/"]
}
```
then, adding TypeScript Testing Infrastructure

```
yarn add -D ts-jest typescript
```
jest `package.json`

```json
  "jest": {
    "preset": [
      "react-native",
      "jest-expo"
    ],
    "transform": {
      "^.+\\.jsx?$": "<rootDir>/node_modules/babel-jest",
      "^.+\\.tsx?$": "ts-jest",
      "\\.(ts|tsx)$": "<rootDir>/node_modules/ts-jest/preprocessor.js"
    },
    "testRegex": "(/__tests__/.*|(\\.|/)(test|spec))\\.(jsx?|tsx?)$",
    "testPathIgnorePatterns": [
      "\\.snap$",
      "<rootDir>/node_modules/",
      "<rootDir>/lib/"
    ],
    "moduleFileExtensions": [
      "ts",
      "tsx",
      "js",
      "jsx",
      "json",
      "node"
    ],
    "cacheDirectory": ".jest/cache",
    "globals": {
      "ts-jest": {
        "useBabelrc": true
      }
    }
```

now, enjoy your TypeScript Type React-Native

[jest]:https://github.com/kulshekhar/ts-jest#react-native
[ts]:https://github.com/Microsoft/TypeScript-React-Native-Starter
[udtrokia]: https://github.com/udtrokia/React-Native-TypeScript-Starter
