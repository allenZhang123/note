##babel转码器

###配置.babelrc

```
  {
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
  }
```
转码规则：

```
# ES2015转码规则
$ npm install --save-dev babel-preset-es2015

# react转码规则
$ npm install --save-dev babel-preset-react

# ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3
```

###命令行转码babel-cli

安装：

```
$ npm install --global babel-cli
```

在命令行全局转码：

```
# 转码结果输出到标准输出
$ babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib

# -s 参数生成source map文件
$ babel src -d lib -s
```

在项目中转码：

```
# 安装
$ npm install --save-dev babel-cli
```
更改package.json，添加build

```
{
  // ...
  "devDependencies": {
    "babel-cli": "^6.0.0"
  },
  "scripts": {
    "build": "babel src -d lib"
  },
}
```
转码的时候，就执行下面的命令。

```
$ npm run build
```
###babel-node REPL环境

babel-cli工具自带一个babel-node命令，提供一个支持ES6的REPL环境。

它支持Node的REPL环境的所有功能，而且可以直接运行ES6代码。

```
$ babel-node
> (x => x * 2)(1)
2

# babel-node命令可以直接运行ES6脚本。将上面的代码放入脚本文件es6.js，然后直接运行。
$ babel-node es6.js
2

# babel-node也可以安装在项目中。
$ npm install --save-dev babel-cli

# 然后，改写package.json。
{
  "scripts": {
    "script-name": "babel-node script.js"
  }
}
上面代码中，使用babel-node替代node，这样script.js本身就不用做任何转码处理。
```

###babel-register

babel-register模块改写require命令，为它加上一个钩子。此后，每当使用require加载.js、.jsx、.es和.es6后缀名的文件，就会先用Babel进行转码。

```
$ npm install --save-dev babel-register

// 使用时，必须首先加载babel-register。
require("babel-register");
require("./index.js");
// 然后，就不需要手动对index.js转码了。
```

需要注意的是，babel-register只会对require命令加载的文件转码，而不会对当前文件转码。

另外，由于它是实时转码，所以只适合在开发环境使用。

###babel-core

调用Babel的API进行转码

```
#安装
npm install babel-core --save

// 使用
var babel = require('babel-core');

// 字符串转码
babel.transform('code();', options);
// => { code, map, ast }

// 文件转码（异步）
babel.transformFile('filename.js', options, function(err, result) {
  result; // => { code, map, ast }
});

// 文件转码（同步）
babel.transformFileSync('filename.js', options);
// => { code, map, ast }

// Babel AST转码
babel.transformFromAst(ast, code, options);
// => { code, map, ast }
// 配置对象options，可以参看官方文档http://babeljs.io/docs/usage/options/。

// 下面是一个例子。

var es6Code = 'let x = n => n + 1';
var es5Code = require('babel-core')
  .transform(es6Code, {
    presets: ['es2015']
  })
  .code;
// '"use strict";\n\nvar x = function x(n) {\n  return n + 1;\n};'
// 上面代码中，transform方法的第一个参数是一个字符串，表示需要被转换的ES6代码，第二个参数是转换的配置对象。
```

###babel-polyfill

Babel默认只转换新的JavaScript句法（syntax），而不转换新的API，比如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码。

举例来说，ES6在Array对象上新增了Array.from方法。Babel就不会转码这个方法。如果想让这个方法运行，必须使用babel-polyfill，为当前环境提供一个垫片。

```
#安装
$ npm install --save babel-polyfill

// 然后，在脚本头部，加入如下一行代码。
import 'babel-polyfill';
// 或者
require('babel-polyfill');
```

###浏览器环境

**方法一：**

Babel也可以用于浏览器环境。但是，从Babel 6.0开始，不再直接提供浏览器版本，而是要用构建工具构建出来。如果你没有或不想使用构建工具，可以通过安装5.x版本的babel-core模块获取。

`$ npm install babel-core@5`
运行上面的命令以后，就可以在当前目录的node_modules/babel-core/子目录里面，找到babel的浏览器版本browser.js（未精简）和browser.min.js（已精简）。

然后，将下面的代码插入网页。

```
<script src="node_modules/babel-core/browser.js"></script>
<script type="text/babel">
// Your ES6 code
</script>
```
上面代码中，browser.js是Babel提供的转换器脚本，可以在浏览器运行。用户的ES6脚本放在script标签之中，

但是要注明 **type="text/babel"**。

**方法二：**

使用babel-standalone模块提供的浏览器版本，将其插入网页。

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.4.4/babel.min.js"></script>
<script type="text/babel">
// Your ES6 code
</script>
```
注意，网页中实时将ES6代码转为ES5，对性能会有影响。生产环境需要加载已经转码完成的脚本。

**方法三：**

下面是如何将代码打包成浏览器可以使用的脚本，以Babel配合Browserify为例。首先，安装babelify模块。

```
$ npm install --save-dev babelify babel-preset-es2015

# 然后，再用命令行转换ES6脚本。
$  browserify script.js -o bundle.js \
  -t [ babelify --presets [ es2015 ] ]
# 上面代码将ES6脚本script.js，转为bundle.js，浏览器直接加载后者就可以了。

# 在package.json设置下面的代码，就不用每次命令行都输入参数了。
{
  "browserify": {
    "transform": [["babelify", { "presets": ["es2015"] }]]
  }
}
```

###Traceur转码器

Google公司的Traceur转码器，也可以将ES6代码转为ES5代码

[链接——阮一峰](http://es6.ruanyifeng.com/#docs/intro#Traceur转码器)