# 关于array

[MDN-Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

## length问题

```js
var a = [];
a['b'] = 1;
console.log(a);  // [b: 1]
console.log(a.length);  // 0

a['2'] = 2;
console.log(a);  // [empty × 2, 2, b: 1]
console.log(a.length);  // 3
a.length = 0;
console.log(a);  // [b: 1]
```

看着上面的代码，觉得有点混乱，这是什么鬼？？？

我们在控制台输入下面的代码：

```js
var b = [1, 2, 3, 4];
b[2];  // 3
b["2"];  // 3
b["02"];  // undefined
```

原来，b[2] 中的 2 会被 JavaScript 解释器通过调用 toString 隐式转换成字符串，所以 `b[2] == b['2']`。那么最上面的问题就不难解决了。

# 闭包

题目如下：

```js
for(var i = 0; i < 5; i++){
  //代码，输出0到4，考闭包
}
```

解决方法：

```js
for(var i = 0; i < 5; i++){
  (function(j) {
    setTimeout(function() {
      console.log(j);
    }, 1000);
  })(i);
}
```

要是面试官没要求一定要用 `var`，那么我们可以使用 es6 新特性 `let`：

```js
for(let i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}
```

要是他要一秒一秒的输出呢？

> 第一种

```js
for(var i = 0; i < 5; i++) {
  (function(j) {
    setTimeout(function() {
      console.log(j);
    }, 1000 * j);
  })(i);
}
```

> 第二种

```