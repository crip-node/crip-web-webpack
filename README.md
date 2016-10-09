# cripweb-webpack
[CripWeb](https://github.com/crip-node/crip-web) extension to use with [webpack](https://webpack.github.io/)

## Configurations

For configuration you can use cripweb configuration module.
Default configuration definition: 
```js
{
  webpack: {
    base: '',
    output: '{assetsDist}',
    config: {},
    isInDefaults: true
  }
}
```

## Sample of usage

```js
var gulp = require('gulp');
var cripweb = require('cripweb');
var cripwebWebpack = require('cripweb-webpack');

// define your own webpack config or require existing one by `require('./webpack.config.js')`
var webpack_config = {
  entry: './assets/src/index.tsx',
  ...
};

cripweb(gulp)(function (crip) {
  // define external crip plugin for webpack
  crip.define('webpack', cripWebpack);

  // now you have available webpack configuration
  crip.config.set('webpack', {
    output: '{assetsDist}\\js',
    config: webpack_config
  });
  
  // now we can define our webpack configuration
  crip.webpack('typescripts', 'assets/src/**/*.tsx');
});
```

## Definition webpack(taskName, globs [ [, webpackConfig], outputPath [, prependPath] ])

#### taskName
Type: `string`

Task name for gulp output. Will be prefixed with `webpack-` to be unique in gulp.

#### globs
Type: `string` or `array`

Glob or array of globs to be read and listenned on `watch-globs` task.

#### webpackConfig
Type: `object`

[Webpack configuration file](http://webpack.github.io/docs/tutorials/getting-started/#config-file).

#### outputPath
Type: `string`

Location where webpack output files will be located.

#### prependPath
Type: `string`

The place where patterns starting with / will be mounted onto `globs` items.
By default is used configuration `webpack.base` value (`empty string`).
