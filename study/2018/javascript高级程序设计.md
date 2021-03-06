#

indexdDb最大的特点就是使用对象保存数据，而不是使用表来保存数据，一个indexdDb就是一组位于相同命名空间下的对象集合。


### 可维护性：

可理解、直观、适应性、可扩展性

### 代码约定
1. 可读性：缩进、注释（函数和方法、大段代码、复杂的算法、Hack）
2. 变量和函数命名：变量名应为名词、函数名应以动词开始；布尔值以is开始；变量和函数名都应使用合乎逻辑的名字，不要担心长度；
3. 变量类型透明（初始值、注释）

### 松耦合
HTML与Javascript;CSS与Javascript;应用逻辑与事件处理程序

### 编程实践

最佳实践是永远不修改不属于你的对象，你不能预期未来浏览器会拥有者会作何改变

避免与null比较，必须按照被期望的值进行检查，而非不期望
代码中的null比较越小，就越容易达到代码的目的，并且消除不必要的问题。

对于企业级的JavaScript开发而言，使用常量是非常重要的技巧，因为它能让代码更容易维护，并在数据更改的同时保护代码。


避免全局变量，使用常量

### 性能

1. 注意作用域、避免全局查找
2. 避免with，会创建自己的作用域、增加作用域链的长度，代码执行速度比外面的慢
3. 使用变量和数组要比访问对象上的属性更有效率，后者是一个O(n)的操作
4. 优化循环
5. 原生方法快、Switch语句快、位运算快
6. 最小化语句数
7. 插入迭代值：

```
var name = values[i];
i++;
//转为
var name = values[i++];
```

8. 优化DOM交互（最小化现场更新：合并innerHTML）
9. 使用事件代理
10. HTMLCollection问题

### 部署
1. 构建
2. 验证
3. 压缩（文件、HTTP）

setTimeout与setInterval有相同的问题，他们的第二个参数，只是将任务插入到UI任务队列的时间，如果UI线程繁忙，比如响应用户操作，那么任务就不会立即执行

### new API

requestAnimationFrame
Page Visibility API
File API
Geolocation API
Web Timing
Web Workers

解构赋值：

```
var value1 = 5;
var value2 = 10;
[value2, value1] = [value1, value2]                                                                                                                                                                                         
```

### 柯里化和绑定函数
JavaScript中的柯里化函数和绑定函数提供了强大的动态函数创建功能。使用bind()还是curry()要根据是否需要object对象响应来决定。它们都能用于创建复杂的算法和功能，当然两者都不能滥用，因为每个函数都会带来额外的开销。

### 服务推送事件 SSE
未实践


this对象是在运行时基于函数的执行环境绑定的：在全局函数中，this等于window，而当函数作为某个对象的方法调用时，this等于那个对象,但是对象的方法内部如果还有其他函数，那此函数里的this也是指向window，不论具名与否。匿名函数具有全局性。
箭头函数根本没有自己的this，而是引用外层代码块的this

每个函数都有自己的执行环境。当执行流进入一个函数时，函数的环境会被推入一个环境栈中，而在函数执行之后，栈将其环境弹出，把控制权返回给之前的执行环境。