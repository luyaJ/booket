> Array.from()

从一个类似数组或可迭代对象中创建一个新的数组实例。

```js
`Array from a String`
Array.from('foo');   // ["f", "o", "o"]

// Array from a Set
let s = new Set(['foo', window]);
Array.from(s);   // ["foo", Window]

// Array from a Map
let m = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(m);   // [[1, 2], [2, 4], [4, 8]]

// Array from an Array-like object(arguments)
function f() {
  return Array.from(arguments);
}
f(1, 2, 3);   // [1, 2, 3]
```