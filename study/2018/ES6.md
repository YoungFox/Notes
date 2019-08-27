//解构赋值
```
let {length : len} = 'hello';
len // 5
```

<!--解构赋值提取JSON-->
let jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};

let { id, status, data: number } = jsonData;

console.log(id, status, number);


let {floor,ceil} = Math;
floor(1.1)

<!--补全时间-->
'1'.padStart(10, '0') // "0000000001"
'12'.padStart(10, '0') // "0000000012"


模板字符串也能循环



let sender = '<script>alert("abc")</script>'; // 恶意代码

let message =
  SaferHTML`<p>${sender} has sent you a message.</p>`;

function SaferHTML(templateData) {
  let s = templateData[0];
  for (let i = 1; i < arguments.length; i++) {
    let arg = String(arguments[i]);

    // Escape special characters in the substitution.
    s += arg.replace(/&/g, "&amp;")
            .replace(/</g, "&lt;")
            .replace(/>/g, "&gt;");

    // Don't escape special characters in the template.
    s += templateData[i];
  }
  return s;
}



这样做的目的，是逐步减少全局性方法，使得语言逐步模块化。
Number.parseInt === parseInt // true
Number.parseFloat === parseFloat // true


rest参数， ...params

扩展运算符 ... 和rest长得一模一样！！！将数组变为参数序列。内部调用了Iterator接口

Math.max(...[14, 3, 77])



这就叫做“尾调用优化”（Tail call optimization），即只保留内层函数的调用帧。如果所有函数都是尾调用，那么完全可以做到每次执行时，调用帧只有一项，这将大大节省内存。这就是“尾调用优化”的意义。
且尾函数不能调用外层函数内的变量


Array.from: 将对象转为真正的数组。
Array.of: 将一组值转为数组

Iterator接口主要供for...of消费


WeakMap的设计目的在于，有时我们想在某个对象上面存放一些数据，但是这会形成对于这个对象的引用。WeakMap 就是为了解决这个问题而诞生的，它的键名所引用的对象都是弱引用，即垃圾回收机制不将该引用考虑在内。因此，只要所引用的对象的其他引用都被清除，垃圾回收机制就会释放该对象所占用的内存。也就是说，一旦不再需要，WeakMap 里面的键名对象和所对应的键值对会自动消失，不用手动删除引用。



执行 Generator 函数会返回一个遍历器对象，也就是说，Generator 函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历 Generator 函数内部的每一个状态。

ES6 诞生以前，异步编程的方法，大概有下面四种。
		回调函数
		事件监听
		发布/订阅
		Promise 对象


async await
并列多个await，需要等await都完成才会继续后续的操作。



AMD commonJS UMD

AMD:define
commonJS: module.exports ,require
UMD: 整合上面两个，如果都不存在则使用兼容模式window.xx



Object.defineProperty(obj, prop, descriptor)

如果一个描述符不具有value,writable,get 和 set 任意一个关键字，那么它将被认为是一个数据描述符。如果一个描述符同时有(value或writable)和(get或set)关键字，将会产生一个异常。

