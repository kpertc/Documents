#web-dev 

Install Webpack
``` shell
npm i -D webpack webpack-cli
```

package.json
```json
"scripts": { 
	"build": "webpack --mode production" 
}
```



``` json
module.exports = {
	mode: 'development', 
	entry:{

	}

	output:{
	
	}

	// loader scss
	module: {
		test: /\.scss$/,
		use: ['style-loader', 'css-loader', 'sass-loader'] 
	}

	plugin: [
		
	]
}
```