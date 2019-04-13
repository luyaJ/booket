鲜为人知，Array.prototype 也是一个数组。

## 检测数组：instanceof 和 isArray

当检测Array实例时，`Array.isArray` 优于 `instanceof`，因为 `Array.isArray` 可以检测 `iframes`。

> Array.from()

从一个类似数组或可迭代对象中创建一个新的数组实例。

```js
// Array from a String
Array.from('foo');   
// ["f", "o", "o"]

// Array from a Set
let s = new Set(['foo', window]);
Array.from(s);   
// ["foo", Window]

// Array from a Map
let m = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(m);   
// [[1, 2], [2, 4], [4, 8]]

// Array from an Array-like object(arguments)
function f() {
  return Array.from(arguments);
}
f(1, 2, 3);   
// [1, 2, 3]

// Using arrow function and Array.from
Array.from([1, 2, 3], x => x + x);
// [2, 4, 6]
Array.from({length: 5}, (v, i) => i);
// [0, 1, 2, 3, 4]

// 数组去重合并
function combine() { 
  let arr = [].concat.apply([], arguments); 
  return Array.from(new Set(arr)); 
}
var m = [1, 2, 2], n = [2, 3, 3];
// [1, 2, 3]
```

> Array.isArray()

用来判断传递的值是否是一个 `Array`。

```js
// 返回true
Array.isArray([]);
Array.isArray([1, 2]);
Array.isArray(new Array());
Array.isArray(Array.prototype);

// 返回false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(17);
Array.isArray('foo');
Array.isArray(true);
Array.isArray(false);
Array.isArray({__proto__: Array.prototype});
```

> Array.of()

创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。

```js
Array.of(7);        // [7]
Array.of(1, 2, 4);  // [1, 2, 4]

Array(7);           // [ , , , , , , ]
Array(1, 2, 4);     // [1, 2, 4]
```

这两个的区别在于处理整数参数：`Array.of(7)` 创建一个具有单个元素 7 的数组，而 `Array(7)` 创建一个长度为 7 的空数组（注意是：有7个空位的数组，而不是由7个undefined组成的数组）。

> Array.prototype.concat()

用于合并两个或多个数组。这个方法不会改变原数组，只会返回一个新数组。

```js
// 连接两个数组
var a = ['a','b','c'];
var num = [1, 2, 3];
a.concat(num);  // ["a", "b", "c", 1, 2, 3]

// 连接三个数组
var c = [2, 4, 6];
a.concat(num, c);  // ["a", "b", "c", 1, 2, 3, 2, 4, 6]

// 将值连接到数组
a.concat(1, [2, 3]);  // ["a", "b", "c", 1, 2, 3]

// 合并嵌套
var n1 = [[1]];
var n2 = [2, [3]];
a1 = n1.concat(n2);
console.log(a1);  // [[1], 2, [3]]
a2 = n1[0].push(4);
console.log(a2);  // 2 (返回的是length = 2)
console.log(n1);  // [1, 4]
```

> Array.prototype.copyWithin()

语法：`arr.copyWithin(target[, start[, end]])`

浅复制数组的一部分到同一个数组中的另一个位置，即**将start到end之间指定的子元素复制到arr中target指定的开始位置**，并返回它，而不修改它的大小。

* `target`： 0为基底的索引，复制序列到该位置。如果是负数，`target` 将从末尾开始计算。
* `start`：0为基底的索引，开始复制元素的起始位置。如果是负数，`start` 将从末尾开始计算。
* `end`：0为基底的索引，开始复制元素的结束位置。如果是负数，`start` 将从末尾开始计算。

```js
// 从索引为2开始，开始复制索引为0的数，直到结尾
[1, 2, 3, 4, 5].copyWithin(2);   // [1, 2, 1, 2, 3]

[1, 2, 3, 4, 5].copyWithin(-2);  // [1, 2, 3, 1, 2]

[1, 2, 3, 4, 5].copyWithin(0, 2);  // [3, 4, 5, 4, 5]

[1, 2, 3, 4, 5].copyWithin(0, 2, 3);  // [3, 4, 3, 4, 5]

[1, 2, 3, 4, 5].copyWithin(-2, -3, -1);  // [1, 2, 3, 3, 4]

[].copyWithin.call({length: 5, 3: 1}, 0, 3);  // {0: 1, 3: 1, length: 5}
```

> Array.prototype.entries()

返回一个新的 Array Iterator 对象，该对象包含数组中每个索引的键/值对。