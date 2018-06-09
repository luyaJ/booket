## null和undefined的区别

null就是空，如果定义`var flag = null;`，那么这个flag的值就是空值，打印出来为`null`。

undefined表示未定义，`var flag;`，将flag打印出来结果为`undefined`。

所以两者的区别就是：
* 一个是已经定义可是却为空，一个是未定义是何种类型的。
* `null`转为数字类型值为0，`undefined`转为数字类型`NaN`
* 设置为`null`的变量或者对象会被内存收集器回收

```js
var flag1;
var flag2 = null;

flag1  // undefined
flag2  // null

flag1 == null;  // true
flag1 == undefined;  // true
flag1 == flag2;  // true
flag1 === flag2;  // false

flag2 == null;  // true
flag2 == "null";  // false
flag2 == "undefined";  // false
```

**null==undefined结果是true的，null===undefined结果是false的**