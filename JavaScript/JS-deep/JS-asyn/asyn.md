## JS 异步编程

> JS 大量IO操作下的异步编程

所谓的异步指的是函数的调用并不直接返回执行的结果，而往往是通过回调函数异步的执行。

### 参考

- [Javascript异步编程](http://www.jianshu.com/p/6d4d2e21d041)

### 了解

```
// 回调函数 示例

var fn = function(callback) {
    // do something here
    ...
    callback.apply(this, this.arguments);
}
 
var mycallback = function(parameter) {
    // do someting in customer callback
}
 
// call the fn with callback as parameter
fn(mycallback);

// 异步示例

setTimeout(function(){
    console.log("this will be exectued after 1 second!");
},1000);

```

>Javascript通过事件驱动机制，在单线程模型下，以异步回调函数的形式来实现非阻塞的IO操作。

**回调地域**

```
operation1(function(err, result) {
    operation2(function(err, result) {
        operation3(function(err, result) {
            operation4(function(err, result) {
                operation5(function(err, result) {
                    // do something useful
                })
            })
        })
    })
})
```

**流程控制**

```
var urls = ['url1','url2','url3'];
var result = [];
 
for (var i = 0, len = urls.length(); i < len; i++ ) {
    $.ajax({
        url: urls[i],
        context: document.body,
        success: function(){
          //do something on success
          result.push("one of the request done successfully");
          if (result.length === urls.length()) {
              //do something when all the request is completed successfully
          }
        }});
}
```

promise 优化

```
operation1().then(function (result1) {
    return operation2(result1)
}).then(function (result2) {
    return operation3(result2);
}).then(function (result3) {
    return operation4(result3);
}).then(function (result4) {
    return operation5(result4)
}).then(function (result5) {
    //And so on
});
```