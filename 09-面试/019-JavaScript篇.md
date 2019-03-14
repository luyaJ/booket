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

# Buffer

为了使 `Buffer` 实例的创建更可靠，`new Buffer()` 构造函数已被废弃，建议使用 `Buffer.from()`、`Buffer.alloc()`。

### Buffer.alloc(length)

```js
var buf1 = Buffer.alloc(10);  // 长度为10的buffer，初始值为0x0
var buf2 = Buffer.alloc(10, 1);  // 长度为10的buffer，初始值为0x1

var buf3 = Buffer.allocUnsafe(10);  // 长度为10的buffer，初始值不确定

var buf4 = Buffer.from([1, 2, 3]);  // 长度为3的buffer，初始值为0x01,0x02,0x03
```

* Buffer.from(array) 返回一个 Buffer，包含传入的字节数组的拷贝。
* Buffer.from(string[, encoding]) 返回一个 `Buffer`，包含传入的字符串的拷贝。