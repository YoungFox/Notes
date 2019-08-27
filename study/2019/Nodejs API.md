Node.js 不检查 Content-Length 和已传输的主体的长度是否相等。

##process

process 对象是一个全局变量，它提供有关当前 Node.js 进程的信息并对其进行控制。 作为一个全局变量，它始终可供 Node.js 应用程序使用，无需使用 require()。

正确使用 'uncaughtException' 事件的方式，是用它在进程结束前执行一些已分配资源（比如文件描述符，句柄等等）的同步清理操作。 触发 'uncaughtException' 事件后，用它来尝试恢复应用正常运行的操作是不安全的。

想让一个已经崩溃的应用正常运行，更可靠的方式应该是启动另外一个进程来监测/探测应用是否出错， 无论 uncaughtException 事件是否被触发，如果监测到应用出错，则恢复或重启应用。

##Error

JavaScript 的 throw 机制的任何使用都会引起异常，异常必须使用 try / catch 处理，否则 Node.js 进程会立即退出。

##stream

Node.js 提供了多种流对象。 例如，HTTP 服务器的请求和 process.stdout 都是流的实例。


##global
