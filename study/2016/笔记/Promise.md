Promise

### 生命周期：

1. pending :未完成，执行中

2.Fulfilled or Rejected



### 使用then()监听fulfilled和Rejected，而且是任意多个，任意组合
如：

```
let promise = readFile("example.txt");

promise.then(function(contents) {
    // fulfillment
    console.log(contents);
}, function(err) {
    // rejection
    console.error(err.message);
});

promise.then(function(contents) {
    // fulfillment
    console.log(contents);
});

promise.then(null, function(err) {
    // rejection
    console.error(err.message);
});
```

catch()只监听Rejected

```
promise.catch(function(err) {
    // rejection
    console.error(err.message);
});

// is the same as:

promise.then(null, function(err) {
    // rejection
    console.error(err.message);
});
```

即使promise已经完成，依然可以添加处理器（handlers），而且保证可以执行（状态匹配的情况下）。

例如：
```
let promise = readFile("example.txt");

// original fulfillment handler
promise.then(function(contents) {
    console.log(contents);

    // now add another
    promise.then(function(contents) {
        console.log(contents);
    });
});
```

Rejection也是一样。

###未处理的（unsettled）promise

使用Promise构造器（constructor）新建promises对象，构造器只接受一个参数，名为executor的函数，函数需要两个参数resole()和reject(),分别是promise解决或者失败会执行的方法。

new的时候executor会立即执行，当resole或reject执行时，都会在作业队列（job queue）添加一个job来解决promise。

```
let promise = new Promise(function(resolve, reject) {
    console.log("Promise");
    resolve();
});

promise.then(function() {
    console.log("Resolved.");
});

console.log("Hi!");
```

结果是

```
Promise
Hi!
Resolved
```

？？？因为fulfillment 和 rejection处理器总会在executor完成后被添加到作业队列尾部。

###已处理的promise

```
let promise = Promise.resolve(42);

promise.then(function(value) {
    console.log(value);         // 42
});
```
上面的例子不会触发rejection


###链式promise


