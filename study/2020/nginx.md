#I/O模型
据说3W并发？

网络IO：本质是socket读取

同步/异步：

同步：synchronous,调用者等待被调用者返回消息，才能继续执行

异步：asynchronous,被调用者通过状态、通知或回调机制主动通知调用者被调用者的运行状态

阻塞/非阻塞

阻塞：blocking,指IO操作需要彻底完成后才返回到用户空间，调用结果返回之前，调用者被挂起

非阻塞：nonblocking,指IO操作被调用后立即返回给用户一个状态值，无需等到IO操作彻底完成，最终的调用结果返回之前，调用者不会被挂起

I/O模型：

阻塞型、非阻塞型、复用型、信号驱动型、异步

软件思想：应用程序承担少一些，内核承担多一些，可以提高程序的承载能力


#nginx模块

分类：

核心模块：core module

标准模块：
	
	HTTP模块：ngx_http_*
		
		HTTP Core modules 默认功能
		HTTP Optional modules 需编译时指定
		
	Mail模块：ngx_mail_*
	Stream模块：ngx_stream_*

第三方模块




default_server


The way nginx and its modules work is determined in the configuration file. By default, the configuration file is named nginx.conf and placed in the directory 

```
/usr/local/nginx/conf
/etc/nginx
/usr/local/etc/nginx.

```
