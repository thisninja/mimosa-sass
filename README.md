mimosa-sass
===========

## Overview

This is a SASS compiler for the Mimosa build tool.

You can use this module for both Ruby SASS and [node-sass](https://github.com/andrew/node-sass).

For more information regarding Mimosa, see http://mimosa.io

Note: Version `1.1.0` works with Mimosa `2.0.8` and above.

Note: Using version `2.0+` with the node-sass compiler requires `1.0+` of that compiler.

## Usage

Add `'sass'` to your list of modules.  That's all!  Mimosa will install the module for you when you start `mimosa watch` or `mimosa build`.

## Functionality

This module will compile SASS files during `mimosa watch` and `mimosa build` and includes compilation with [compass](http://compass-style.org/).

For SASS compilation there are two compiling options, using Ruby SASS ([SASS Ruby gem install)](http://sass-lang.com/) or node.js SASS (via the [node-sass](https://github.com/andrew/node-sass) library).

### Ruby

Ruby is SASS' source language and the node.js version is a port of the Ruby functionality to node.js.

### node-sass

This module does not come bundled with the node.js version as it can occasionally cause installation issues, but this module is ready to use the node version if it is provided. Use the `lib` setting to provide a node-sass compiler. (Ex: `lib: require('node-sass')`). By default the Ruby version is enabled, but if `lib` is provided, node-sass will be used.

### Compass

Compass [(Ruby install)](http://compass-style.org/install/) does not have a node.js port, so to use SASS and Compass together, Ruby SASS must be used.

To install compass: `$ gem install compass`

After that you can add compass features by adding `@import "compass"` into your sass/scss file;
That's all. Just restart your server by command `$ mimosa watch --server` or `$ mimosa watch -s`

### Bourbon

You can also use [Bourbon](http://bourbon.io/).

To install it: `$ gem install bourbon`.

After that you need to type: `bourbon install` in your stylesheets directory (by defult it's "assets/stylesheets/"; it may be configurable in your `mimosa-config` file).

To watch and compile your changes you need to run: `sass --watch sass_directory:css_directory` where `sass_directory` - your sass folder path; `sass_directory` - css output folder path.

By default it will look like: `$ sass --watch assets/stylesheets/:public/stylesheets`.

After that you can simply add bourbon features into your sass/scss file by adding: `@import "bourbon/bourbon"`

## Source Maps

If using node-sass, this module includes support for inline (dynamic) source maps.  Source maps will be created for your compiled sass file and included at the bottom of the compiled CSS.  This is enabled by default for `mimosa watch`.  `mimosa build` is presumed to not be a dev time task, therefore source maps are disabled.

## Default Config

```javascript
sass: {
  sourceMap: true,
  lib: undefined,
  extensions: ["sass", "scss"],
  includePaths: []
}
```

* `sourceMap`, a boolean, whether or not source maps are provided during `mimosa watch` for node-sass compilation.  If you are using Ruby sass, this setting is not used.  If you are running `mimosa build`, set setting is automatically set to `false`.
* `lib`: Using the `lib` property you can provide a node version of SASS. You must have `node-sass` `npm install`ed into your project and then provide it to `lib`. For instance: `lib: require('node-sass')`.
* `extensions`: an array of strings, the extensions of your SASS files.
* `includePaths`: an array of path strings to look for any @imported files.
