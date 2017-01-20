###css-loader

Webpack 本身只能处理 JavaScript 模块，如果要处理其他类型的文件，就需要使用 loader 进行转换。

Loader 可以理解为是模块和资源的转换器，它本身是一个函数，接受源文件作为参数，返回转换的结果。这样，我们就可以通过 require 来加载任何类型的模块或文件，比如 CoffeeScript、 JSX、 LESS 或图片。

安装 loader：

`npm install css-loader style-loader`

css文件:

```
/* style.css */
body { background: yellow; }
```

修改 entry.js：

```
require("!style!css!./style.css") // 载入 style.css
document.write('It works.')
document.write(require('./module.js'))
```
执行：

方法一： `webpack`

方法二：

```
将 entry.js 中的 require("!style!css!./style.css") 修改为 require("./style.css") ，然后执行：

$ webpack entry.js bundle.js --module-bind 'css=style!css'
```
方法三：

配置文件 webpack.config.js

```
var webpack = require('webpack')

module.exports = {
  entry: './entry.js',
  output: {
    path: __dirname,
    filename: 'bundle.js'
  },
  module: {
    loaders: [
      {test: /\.css$/, loader: 'style!css'}
    ]
  }
}
```
同时简化 entry.js 中的 style.css 加载方式：

```
require('./style.css')
```
