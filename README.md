The Vertigo Stack
=================

[![Dependency Status](https://david-dm.org/marvinroger/vertigo-stack.svg?style=flat)](https://david-dm.org/marvinroger/vertigo-stack) [![devDependency Status](https://david-dm.org/marvinroger/vertigo-stack/dev-status.svg?style=flat)](https://david-dm.org/marvinroger/vertigo-stack#info=devDependencies)


![The Vertigo Stack](https://i.imgur.com/VIfziO0.png "The Vertigo Stack")

A modern opinionated web stack that will give you vertigo.

## Overview

This is a web stack using modern bulletproof technologies:

* **[NodeJS](https://nodejs.org/) with [Express 4](http://expressjs.com/)** as backend software
* **[Mocha](https://mochajs.org/) and [Chai](http://chaijs.com/)** as testing framework
* **[ES6-7 (using babel)](https://babeljs.io/)** compiled to ES5 as frontend scripting language
* **[Riot](http://riotjs.com/)** as UI library
* **[Stylus](https://learnboost.github.io/stylus/)** as styling language
* **[Nunjucks](https://mozilla.github.io/nunjucks/)** as templating language
* **[Gulp](https://github.com/gulpjs/gulp/)** as building tool
* **[Wercker](http://wercker.com/)** as CI and Continuous Deployment tool

These technologies allow to be more productive by reducing the amount of code needed, and are all available in NPM, avoiding the need to have another environment like Ruby installed.

## Features

* during development:
  * reload the server when code changed
  * build Stylus and ES6-7 (with module support) with source maps support when code changed
  * BrowserSync anytime something is changed
* during distribution:
  * update humans.txt last updated date
  * CSS autoprefixed
  * JS/CSS minified and cache busted
* goodies:
  * HTML5 Boilerplate-lite with Google Analytics embedded
  * server with compression enabled; threshold set to 1024
  * automatic testing/deployment with Wercker
  * [![js-semistandard-style](https://cdn.rawgit.com/flet/semistandard/master/badge.svg)](https://github.com/Flet/semistandard)

## Installation

* clone the repository: `git clone https://github.com/marvinroger/vertigo-stack.git`
* edit `package.json`
  * pay attention to the `vertigo` key, in which you can configure the Google Analytics ID

## Use

### File tree

```
-- app <- front end code
-- -- css <- stylus files
-- -- -- any stylus files not starting with an `_` will be built in the public/css/ dir
-- -- js <- es6/7 files
-- -- -- app.js <- only entry point of the application (use modules), built at public/js/app.js
-- -- assets <- files not to touch
-- -- -- any files here will be copied as is in the public/ dir
-- -- vendor <- vendor files not to touch
-- -- -- any files here will be copied as is in the public/vendor dir
-- public <- app directory, built
-- views <- back end nunjucks views
-- test <- back end mocha tests

```

### Configuration

#### Wercker *(optional)*

In order to use the CI, the repository must be handled by Wercker by enabling it on the Dashboard.

##### Wercker deployment

In order for Wercker to deploy, a deploy target must be added with the `WERCKER_PRIVATE_KEY` environment variable containing the private key that will connect to the server on which to deploy. The deploy might optionally be triggered automatically on master build success.

### Usage

* `npm start` to start the app in development mode
* `npm test` to unit test the app
* `npm run dev` to start the app in development mode while ES6-7/Stylus/HTML watching with BrowserSync
* `npm run dist` to distribute the app for release
