# 基本数据类型、数组、循环及条件表达式

## 基本数据类型

### 数字

指数表示法：一个数字可以表示成 1e1（或者 1e+1、1E1、1E+1）这样的指数形式，意思就是在数字后面加 1 个 0，也就是 10。同理，2e+3 的意思就是在 2 后面加 3 个 0，也就是2000。

### 字符串

```js
> var s = "some char"
> typeof s
"string"

> var s = "";
> typeof s
"string"
```

当我们在两个数字间使用加号时，执行的是加法计算。但在字符串中，这将会是拼接操作，它返回的是两个字符串拼接后的结果。如下：

```js
> var s1 = 'one';var s2 = 'two'; var s = s1 + s2; s;
"onetwo"
```

**字符串转换**

当我们使用数字字符串进行算术运算过程中，该字符串会在运算中被当做数字类型来使用。

```js
> var s = '1'; s = 3 * s; typeof s;
"number"
> s
3

> var s = '1'; s++; typeof s;
"number"
> s
2
```

于是，将数字字符串转换为数字就有一种偷懒的办法：**只需要将该字符串与 1 相乘即可**。（不过更好的选择是使用 parseInt 函数）

```js
> var s = '100'; s = s * 1;
100
```

同样的，将其他类型转换成字符串也有一种偷懒的方法，只需要将其与空字符串连接即可：

```js
> var n = 1; n = "" + n;
"1"
```

### 比较操作符

`==`：相等运算符（在该比较操作执行之前，两边的操作数会被自动转换成相同类型）

注意，NaN 不等于任何东西，包括自己。

```js
> NaN == NaN
false
```

### undefined和null

```js
> 1*undefined
NaN
> 1*null
0
```

## 数组

如果新元素被添加的位置与原数组末端之间存在一定的间隔，那么这之间的元素将会被自动设定为 undefined 值。

```js
> var a = [1, 2, 4];
> a[6] = 'new';
"new"
> a
[1, 2, 4, empty × 3, "new"]
```

删除元素：

```js
> var a = [1, 2, 3];
> delete a[1];
true
> a
[1, empty, 3]
```

数组的数组：

```js
> var a = [[1, 2, 3], [4, 5, 6]];
> a
[[1, 2, 3], [4, 5, 6]]
> a[0]
[1, 2, 3]
> a[0][0]
1
```

可以通过访问数组方式来获取某个字符串中的特定字符：

```js
> var s = 'one';
> s[0]
"o"
> s[1];
"n"
```

## 条件与循环

我们检查程序中是否存在一个叫做 somevar 的变量，如果存在，就将变量 result 设置为 yes：

```js
> var result = '';
> if(somevar) { result = 'yes'; }
Uncaught ReferenceError: somevar is not defined
> result
""
```

上面这样会返回一个 undefined，所以在检查变量是否存在时，更好的选择是使用 `typeof`。

```js
> if(typeof somevar !== "undefined") { result = 'yes'; }
> result
""
```

**易错点：**

```js
> var a 
> typeof a
"object"

> var s = 'ls'; s++
NaN

> !!"false"
true

> !!undefined
false

> typeof -Infinity
"number"

> 10 % "0"
NaN

> undefined == null
true

> false === ""
false

> typeof "2E+2"
"string"

> a = 3e+3; a++;
3000
```
