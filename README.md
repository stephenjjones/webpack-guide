# Webpack Guide


## Webpack 2

- config file is function instead of object

## CLI

- `$ webpack --progress --config webpack.main --colors`
- Flags:
  * `--progress`
  * `--colors`
  * `--watch`
  * `--display-reasons` => shows info on why modules are included
  * `--display-chunks` => displays any other chunks
  * `--output-library-target`
  * `-d` alias for `--debug --devtool source-map --output-pathinfo` => will output source maps
  * `-p` alias for `--optimize-minimize --optimize-occurence-order` => readies for prod, runs uglify
  * `--profile --json >> stats.json` => output build stats for [analyse tool](https://webpack.github.io/analyse/)

- preLoaders
  * eslint-loader
    preLoaders: [{
      test: /\.jsx?$/,
      loader: "eslint-loader",
      exclude: /node_modules/
    }]

- Plugins
  * webpack.optimize.UglifyJsPlugin
  * webpack.optimize.DefinePlugin
    + define environment variables
  * webpack.optimize.OccurenceOrderPlugin
  * webpack.optimize.AggressiveMergingPlugin

- Vendor
  * separate vendor files used across entry points
  * entry: {
    vendor: [
     'react', 'react-dom'
    ]
  }

- Multiple entry points
  * use separate polyfill chunk to only load when needed in browser that doesn't support (does this work with SSR, should i think)
  entry: {
    common: ["react"],
    polyfill: ["babel/polyfill"]
    /* ... */
  },
  plugins: [new webpack.optimize.CommonsChunkPlugin({ // will extract common modules, js and css
    name: "common",
    minChunks: 2
  })],
  output: {
    path: path.join(__dirname, "public", "js"),
    filename: "[name].js",
    chunkFilename: "[name]_[chunkhash:20].js",
    publicPath: "/js/",
    libraryTarget: "var"
  }

- css with webpack
  * inline css can create flash of content b/c style loader adds with js, instead of css link which is blocking
  * sass-loader (compiles using [libsass, node based]
  * css-loader
  * style-loader (inline css)
  module: {
    test: /\.scss$/,
    loader: "style!css!sass"
  }
  * extract-text-webpack-plugin
    + will create css files named after your entry chunks
  * critical css
    + use require.ensure to async load below the fold content
    + 

## Articles

- [Advanced Webpack Part 1 - CommonsChunk Plugin](http://jonathancreamer.com/advanced-webpack-part-1-the-commonschunk-plugin/)
- [Advanced Webpack Part 2 - Code Splitting](http://jonathancreamer.com/advanced-webpack-part-2-code-splitting/)
- [Advanced Webpack Part 2 - Custom Notifier Plugin](http://jonathancreamer.com/advanced-webpack-part-3-creating-a-custom-notifier-plugin/)
- [Webpack code splitting](http://jonathancreamer.com/webpack-code-splitting-with-es6-and-babel-6/)
- [Automatic code splitting](https://medium.com/modus-create-front-end-development/automatic-code-splitting-for-react-router-w-es6-imports-a0abdaa491e9#.of0hkhrk3)
- [dyanamic route loading - ryan florence](https://medium.com/@ryanflorence/welcome-to-future-of-web-application-delivery-9750b7564d9f#.bgkrp1wzj)
- [webpack 2: tree shaking](https://medium.com/modus-create-front-end-development/webpack-2-tree-shaking-configuration-9f1de90f3233#.v40t86jhs)


## Videos

- [Advanced Webpack](https://www.youtube.com/watch?v=MzVFrIAwwS8)

