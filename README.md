[![npm version](https://img.shields.io/npm/v/@roku-road/eslint-plugin-brs.svg)](https://www.npmjs.com/package/@roku-road/eslint-plugin-brs)
[![Downloads/month](https://img.shields.io/npm/dm/@roku-road/eslint-plugin-brs.svg)](http://www.npmtrends.com/@roku-road/eslint-plugin-brs)
[![Build Status](https://travis-ci.com/RokuRoad/eslint-plugin-brs.svg?branch=master)](https://travis-ci.com/RokuRoad/eslint-plugin-brs)
[![Coverage Status](https://codecov.io/gh/RokuRoad/eslint-plugin-brs/branch/master/graph/badge.svg)](https://codecov.io/gh/RokuRoad/eslint-plugin-brs)
[![Dependency Status](https://david-dm.org/RokuRoad/eslint-plugin-brs.svg)](https://david-dm.org/RokuRoad/eslint-plugin-brs)

The ESLint custom plugin with rules and parser for `.brs` files.


### ESLint plugin for BrightScript

We going to skip the part why linting is important so you can read more about it at [ESLint](https://eslint.org/docs/about) site. Primary motivation for this development is absence of reliable tools for Roku development (at least at the time this work started) and performance criteria.


*Latest tests gave measurement of about 14 seconds for a 1000 files of BrightScript*

This plugin provides parsing and linting tool for your Roku project. While ESLint rules for Javascript are not 1 to 1 replaceable you are able to quickly develop or translate any other rules to work with brightscript. It's written in typescript but could use any JS- technology you like


### Installation

You'll first need to install [ESLint](http://eslint.org):

**With Yarn**

```bash
yarn add --dev eslint
```

**With npm**

```bash
$ npm i eslint --save-dev
```

Next, install `eslint-plugin-brs`:

**With Yarn**
```bash
yarn add --dev eslint-plugin-brs
```

**With npm**
```bash
$ npm install eslint-plugin-brs --save-dev
```

**Note:** If you installed ESLint globally (using the `-g` flag) then you must also install `eslint-plugin-brs` globally.



## Plugin-Provided Rules

*Just as any other project this one requires more feedback and linting rules ideas*


### Parsing and AST

This documentation will be available at https://github.com/RokuRoad/bright


### Writing rules

https://eslint.org/docs/developer-guide/working-with-rules


### Testing rules

Typical test for a rule will look like

Test runner and valid / invalid factories to wrap your test code into testable solution
``` typescript
import { invalidFactory, runTest, validFactory } from '../helpers'
```

Define name of your rule, it will be used to require it and run tests
``` typescript
const RULE_NAME = 'sub-to-function'
```

Provide prefix and suffix, so you can test function body or root element like library import of the function itself
``` typescript
const valid = validFactory(RULE_NAME, '', '')
const invalid = invalidFactory(RULE_NAME, '', '')
```

Define cases to match against. Invalid cases will provide error messages
``` typescript
runTest(RULE_NAME, {
  invalid: [
    [
      `sub a() as Dynamic
      end sub`,

      [ { message: 'Sub a should not have a return type (dynamic). Consider replacing it with Function' } ]
    ]
  ].map(invalid),
  valid: [
    `sub a()
      print a
     end sub
  `
  ].map(valid)
})
```



### SceneGraph
Currently in development, check back soon. Rule will be aware of components tree structure so for instance if function is going to be overwritten or just mistakenly left empty.