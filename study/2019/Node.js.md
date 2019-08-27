http://nqdeng.github.io/7-days-nodejs/#1.1

#NodeJS基础


模块初始化
一个模块中的JS代码仅在模块第一次被使用时执行一次，并在执行过程中初始化模块的导出对象。之后，缓存起来的导出对象被重复利用。

```
var counter1 = require('./util/counter');
var counter2 = require('./util/counter');

console.log(counter1.count());
console.log(counter2.count());
console.log(counter1.count());
console.log(counter2.count());
```

可以看到，counter.js并没有因为被require了两次而初始化两次。


exports
exports对象是当前模块的导出对象，用于导出模块公有方法和属性。别的模块通过require函数使用当前模块时得到的就是当前模块的exports对象。以下例子中导出了一个公有方法。

```
exports.hello = function () {
    console.log('Hello World!');
};
```

module
通过module对象可以访问到当前模块的一些相关信息，但最多的用途是替换当前模块的导出对象。例如模块导出对象默认是一个普通对象，如果想改成一个函数的话，可以使用以下方式。

```
module.exports = function () {
    console.log('Hello World!');
};
```

NodeJS是一个JS脚本解析器，任何操作系统下安装NodeJS本质上做的事情都是把NodeJS执行程序复制到一个目录，然后保证这个目录在系统PATH环境变量下，以便终端下可以使用node命令。

终端下直接输入node命令可进入命令交互模式，很适合用来测试一些JS代码片段，比如正则表达式。

NodeJS使用CMD模块系统，主模块作为程序入口点，所有模块在执行过程中只初始化一次。

除非JS模块不能满足需求，否则不要轻易使用二进制模块，否则你的用户会叫苦连天。

#代码组织和部署

使用npm cache clear可以清空NPM本地缓存，用于对付使用相同版本号发布新版本代码的人。

编写代码前先规划好目录结构，才能做到有条不紊。

稍大些的程序可以将代码拆分为多个模块管理，更大些的程序可以使用包来组织模块。

合理使用node_modules和NODE_PATH来解耦包的使用方式和物理路径。

使用NPM加入NodeJS生态圈互通有无。

想到了心仪的包名时请提前在NPM上抢注。


#文件操作

process是一个全局变量，可通过process.argv获得命令行参数。由于argv[0]固定等于NodeJS执行程序的绝对路径，argv[1]固定等于主模块的绝对路径，因此第一个命令行参数从argv[2]这个位置开始。

学好文件操作，编写各种程序都不怕。

如果不是很在意性能，fs模块的同步API能让生活更加美好。

需要对文件读写做到字节级别的精细控制时，请使用fs模块的文件底层操作API。

不要使用拼接字符串的方式来处理路径，使用path模块。

掌握好目录遍历和文件编码处理技巧，很实用。

#网络操作

http和https模块支持服务端模式和客户端模式两种使用方式。

request和response对象除了用于读写头数据外，都可以当作数据流来操作。

url.parse方法加上request.url属性是处理HTTP请求时的固定搭配。

使用zlib模块可以减少使用HTTP协议时的数据传输量。

通过net模块的Socket服务器与客户端可对HTTP协议做底层操作。

#进程管理

NodeJS可以感知和控制自身进程的运行环境和状态，也可以创建子进程并与其协同工作，这使得NodeJS可以把多个程序组合在一起共同完成某项工作，并在其中充当胶水和调度器的作用。

使用process对象管理自身。

使用child_process模块创建和管理子进程。

###如何控制输入输出

NodeJS程序的标准输入流（stdin）、一个标准输出流（stdout）、一个标准错误流（stderr）分别对应process.stdin、process.stdout和process.stderr，第一个是只读数据流，后边两个是只写数据流，对它们的操作按照对数据流的操作方式即可。例如，console.log可以按照以下方式实现。

```
function log() {
    process.stdout.write(
        util.format.apply(util, arguments) + '\n');
}
```

###异步编程
不掌握异步编程就不算学会NodeJS。

JS本身的throw..try..catch异常处理机制并不会导致内存泄漏，也不会让程序的执行结果出乎意料，但NodeJS并不是存粹的JS。NodeJS里大量的API内部是用C/C++实现的，因此NodeJS程序的运行过程中，代码执行路径穿梭于JS引擎内部和外部，而JS的异常抛出机制可能会打断正常的代码执行流程，导致C/C++部分的代码表现异常，进而导致内存泄漏等问题。

因此，使用uncaughtException或domain捕获异常，代码执行路径里涉及到了C/C++部分的代码时，如果不能确定是否会导致内存泄漏等问题，最好在处理完异常后重启程序比较妥当。而使用try语句捕获异常时一般捕获到的都是JS本身的异常，不用担心上诉问题。

异步编程依托于回调来实现，而使用回调不一定就是异步编程。

JS本身是单线程的，无法异步执行，因此我们可以认为setTimeout这类JS规范之外的由运行环境提供的特殊函数做的事情是创建一个平行线程后立即返回，让JS主进程可以接着执行后续代码，并在收到平行进程的通知后再执行回调函数。除了setTimeout、setInterval这些常见的，这类函数还包括NodeJS提供的诸如fs.readFile之类的异步API。

异步编程下的函数间数据传递、数组遍历和异常处理与同步编程有很大差别。

使用domain模块简化异步代码的异常处理，并小心陷阱。


##总结

要熟悉官方API文档。并不是说要熟悉到能记住每个API的名称和用法，而是要熟悉NodeJS提供了哪些功能，一旦需要时知道查询API文档的哪块地方。

要先设计再实现。在开发一个程序前首先要有一个全局的设计，不一定要很周全，但要足够能写出一些代码。

要实现后再设计。在写了一些代码，有了一些具体的东西后，一定会发现一些之前忽略掉的细节。这时再反过来改进之前的设计，为第二轮迭代做准备。

要充分利用三方包。NodeJS有一个庞大的生态圈，在写代码之前先看看有没有现成的三方包能节省不少时间。

不要迷信三方包。任何事情做过头了就不好了，三方包也是一样。三方包是一个黑盒，每多使用一个三方包，就为程序增加了一份潜在风险。并且三方包很难恰好只提供程序需要的功能，每多使用一个三方包，就让程序更加臃肿一些。因此在决定使用某个三方包之前，最好三思而后行。
