##运行coffee文件

###直接运行文件

**demo.coffee**

`console.log "hello coffeesccript"`

**命令行**

```
coffee demo.coffee
hello coffeesccript
```

###node中运行

**index.js**

```
require('coffee-script');
var hello = require('./demo.coffee');
```
**命令行**

`node index.js`