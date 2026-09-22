#web-dev 

Install Webpack
``` shell
npm i -D webpack webpack-cli
```


### `package.json`
set command to run webpack
```json
"scripts": { 
	"build": "webpack --mode production" 
}
```



``` js
const path = require('path'); // use path module

module.exports = {
	mode: 'development', 
	// entry: './src/index.jsx',
	entry: path.resolve(__dirname, 'src/index.js'),
	output: {
		path: path.resolve(__dirname, 'dist'), // `__dirname` returns the the directory name
		filename: 'index.js',
	},

	// loader scss
	module: {
		rules: [
			{
				test: /\.scss$/,
				use: ['style-loader', 'css-loader', 'sass-loader'] 
			}
		]
	},

	plugins: [
		
	]
}
```


```js
entry: './src/index.jsx',
output: {
	path: path.resolve(__dirname, 'dist'), // `__dirname` returns the the directory name
	filename: 'index.js',
},
```

`externals` - specify dependencies that should not be resolved and bundled by Webpack.

```js
externals: { three: 'THREE' } // provided by CDN / host page, bundling it would duplicate it
```

``` js
const { EnvironmentPlugin, DefinePlugin } = require('webpack')
```
### Define Global Variable
``` javascript
plugins: [
	// Define Global Variable
	// DefinePlugin = raw text substitution, string values need JSON.stringify()
	 new DefinePlugin({
		 IS_PRODUCTION: false,
	 }),
	 // Define Environment Variable
	 new EnvironmentPlugin({
		NODE_ENV: 'development', // use 'development' unless process.env.NODE_ENV is defined
		DEBUG: false,
	}),
]
```

``` ts
declare var IS_PRODUCTION: boolean
console.log(IS_PRODUCTION)
```

Define Environment Variable

webpack 5: no automatic Node core-module polyfills (`fs`, `path`, `crypto`) - configure `resolve.fallback` manually.
