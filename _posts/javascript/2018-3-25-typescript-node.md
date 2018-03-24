---
layout: post
title: Import Node Module in Typescript
categories: typescript
---

# Install your node modules

```
yarn add -D @types/node
```  

# Add types

```json
{
    "compilerOptions":{
        "module": "commonjs",
        "types": ["node"]
    }
}

```  

# tsconfig

```json
{
  "compilerOptions": {
    /* Basic Options */
    "target": "es5",                          /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017','ES2018' or 'ESNEXT'. */
    "module": "commonjs",                     /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext'. */
    "allowJs": false,                       /* Allow javascript files to be compiled. */
    "declaration": true,                   /* Generates corresponding '.d.ts' file. */
    "outDir": "./src",                        /* Redirect output structure to the directory. */
    
    /* Strict Type-Checking Options */
    "strict": true,                           /* Enable all strict type-checking options. */
    "noImplicitAny": true,                 /* Raise error on expressions and declarations with an implied 'any' type. */
    "strictNullChecks": true,              /* Enable strict null checks. */
    "strictFunctionTypes": true,           /* Enable strict checking of function types. */
    "strictPropertyInitialization": true,  /* Enable strict checking of property initialization in classes. */
    "noImplicitThis": true,                /* Raise error on 'this' expressions with an implied 'any' type. */
    "alwaysStrict": true,                  /* Parse in strict mode and emit "use strict" for each source file. */

    /* Additional Checks */
    "noUnusedLocals": true,                /* Report errors on unused locals. */
    "noUnusedParameters": true,            /* Report errors on unused parameters. */
    "noImplicitReturns": true,             /* Report error when not all code paths in function return a value. */
    "noFallthroughCasesInSwitch": true,    /* Report errors for fallthrough cases in switch statement. */

    /* Module Resolution Options */
    "baseUrl": "./",                       /* Base directory to resolve non-absolute module names. */
    "esModuleInterop": true                   /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */

    /* Source Map Options */
    
    /* Experimental Options */
  },
  "include":["./ts"],
  "exclude":[]
}

```
