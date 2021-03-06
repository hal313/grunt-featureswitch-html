[![Build Status](https://travis-ci.org/hal313/grunt-featureswitch-strip.svg?branch=master)](https://travis-ci.org/hal313/grunt-featureswitch-strip)
[![npm version](https://badge.fury.io/js/grunt-featureswitch-strip.svg)](https://badge.fury.io/js/grunt-featureswitch-strip)

# grunt-featureswitch-strip

>This project has been deprecated. Please use [feature-switch-core](https://github.com/hal313/featureswitch-js-functional-example) moving forward.

>Strips disabled features from files as a grunt task. The features are described within specialized HTML or Javascript comments.

## Getting Started
This plugin requires Grunt `~0.4.5`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-featureswitch-strip --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of Javascript:

```js
grunt.loadNpmTasks('grunt-featureswitch-strip');
```

## The "featureswitch-strip" task

### Overview
In your project's Gruntfile, add a section named `featureswitch-strip` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  `featureswitch-strip`: {
    options: {
        includeHTML: true, // Remove features specified with HTML comments (default true)
        includeJS: false   // Remove features specified with Javascript comments (default false)
    },
    features: 'features,json',
    files: [{
      expand: true,
      cwd: 'src',
      src: ['*.html', 'js/*.js'],
      dest: './tmp/'
    }]
  },
});
```

### Options

#### options.includeJS
Type: `boolean`
Default value: `false`

Remove features specified with Javascript comments. Such a feature may look like:
```js
    var username = window.prompt('Username');
    // FEATURE.start(capitalizeInput) //
    username = username.toUpperCase();
    // FEATURE.end(capitalizeInput) //
```
Note that the parser *requires* the trailing ```//``` on the ```// FEATURE.end(...) //``` declaration; this ensures that the parser removes any trailing characters and does not leave unwanted characters in the output.

#### options.includeHTML
Type: `boolean`
Default value: `true`

Remove features specified with HTML comments. HTML features are specified like:
```html
<h1>Frankenstein<h1>
<!-- FEATURE.start(showSubTitle) -->
<h2>or, The Modern Prometheus</h2>
<!-- FEATURE.end(showSubTitle) -->
```
Note that the parser *requires* the trailing ```-->``` on the ```<!-- FEATURE.end(...) -->``` declaration; this ensures that the parser removes any trailing characters and does not leave unwanted characters in the output.

#### features
Type: `Object` or `string`
Default value: `{}`

Defines the features to use. Either as an object with all `boolean` values or the path to a JSON file containing a similar object.

#### files
Type: `string[]`
Default value: `[]`

Standard `grunt` file declaration.

### Usage Examples
In this example, the file index.html is stripped of any feature switch comments, both HTML and Javascript.

```js
grunt.initConfig({
  'featureswitch-strip': {
    options: {
      includeJS: true
    },
    features: {
      f1: false
    },
    files: [{
      expand: true,
      cwd: 'src',
      src: ['*.html', 'js/*.js'],
      dest: './tmp/'
    }]
  }
});
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).
