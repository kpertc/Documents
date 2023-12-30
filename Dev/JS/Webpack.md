#web-dev 

Install Webpack
``` shell
npm i -D webpack webpack-cli
```


### package.json
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