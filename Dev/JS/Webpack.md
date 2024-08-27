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
		test: /\.scss$/,
		use: ['style-loader', 'css-loader', 'sass-loader'] 
	}

	plugin: [
		
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

specify dependencies that should not be resolved and bundled by Webpack.

``` js
const { EnvironmentPlugin, DefinePlugin } = require('webpack')
```
### Define Global Variable
``` javascript
plugin: [
	// Define Global Variable
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
declare var IE_PRODUCTION: boolean
console.log(IE_PRODUCTION)
```

Define Environment Variable
