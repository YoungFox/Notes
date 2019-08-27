CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。

CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。

CommonJS

```
module.exports = {
	a: 1
}

var x = require(./xx);
```

ES6

```
export let counter = 3;

import { counter } from 'xx'
```