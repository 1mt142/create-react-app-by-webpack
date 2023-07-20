#1st Step::

npm init -y

#2nd Step:
```bash
npm i react react-dom
```

```bash
npm i react react-dom
npm i -D @babel/core @babel/preset-env @babel/preset-react babel-loader css-loader html-webpack-plugin sass sass-loader style-loader url-loader webpack webpack-cli webpack-dev-server
```
#3rd Step: Create .bablerc file

```javascript
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

#4 4. Create a webpack.config.js file

```javascript

const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
    output: {
        path: path.join(\_\ _dirname, "/dist"), // the bundle output path
        filename: "bundle.js", // the name of the bundle
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: "src/index.html", // to import index.html file inside index.js
        }),
    ],
    devServer: {
        port: 3030, // you can change the port
    },
    module: {
        rules: [{
                test: /\.(js|jsx)$/, // .js and .jsx files
                exclude: /node_modules/, // excluding the node_modules folder
                use: {
                    loader: "babel-loader",
                },
            },
            {
                test: /\.(sa|sc|c)ss$/, // styles files
                use: ["style-loader", "css-loader", "sass-loader"],
            },
            {
                test: /\.(png|woff|woff2|eot|ttf|svg)\$/, // to import images and fonts
                loader: "url-loader",
                options: {
                    limit: false
                },
            },
        ],
    },
};

```

#5 5. Create an /src folder and create the following files inside it
|-- src
|-- App.js
|-- App.scss
|-- index.html
|-- index.js

## App.js
```javascript
import React from "react";

const App = () => {
   return <h1>Hello React</h1>;
};

export default App;
```


## App.scss

```javascript
h1 {
 color: red;
}
```


## index.html

```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React with Webpack</title>
  </head>
  <body>
    <div id="app"></div>

    <!-- Notice we are pointing to `bundle.js` file -->
    <script src="bundle.js"></script>

  </body>
</html>
```


## index.js

```javascript

import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import "./App.scss";

const el = document.getElementById("app");

ReactDOM.render(<App />, el);

```

## add serve and build script

```bash
"scripts": {
"serve": "webpack serve --mode development",
"build": "webpack --mode production"
},
```


in package.json file

Run the app with

```bash
npm run serve
```

Open your browser on http://localhost:3030/

#Build The App

```bash
npm run build
```
