[教程](http://jiongks.name/blog/vue-code-review/)

function (a:Object,b:Number):Object{}
这种诡异的语法是flowjs提供的类型检测


ast:抽象语法树


defineProperty setter不能设置自身value，否则无限触发setter


queueWatcher 管理watcher队列，独立的，用Promise保证一批一批按序执行。


const ncname = '[a-zA-Z_][\\w\\-\\.]*'
这块看了半天。。。被'[\\w\\-\\.]'这部分整蒙了。。。原来是字符串里先转一下义。。转为"[\w\-\.]"

ncname 的全称是 An XML name that does not contain a colon (:)

nodeType
1:元素
3:文本
8:注释
10:DocumentType

