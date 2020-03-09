JSON (JavaScript Object Notation) 是一种简单的数据格式。

在数据传输流程中，json 是以字符串的形式传递的，而 js 操作的是 json 对象。所以，json 对象和 json 字符串之间的相互转换是关键。

```bash
var str = '{"key": "value"}';  // json字符串
var o = {"key": "value"};  // json对象
```

## json字符串转化为json对象

通过 JSON.parse() 方法解析。

```js
var str = '{"key": "value", "jian": "zhi"}';
var obj = JSON.parse(json);

console.log(obj); // 控制台返回 Object
console.log(obj.key); // 控制台返回 value
console.log(obj.jian); // 控制台返回 zhi
```

## json对象转化为json字符串

```js
var json = '{"key": "value", "jian": "zhi"}';
var obj = JSON.parse(json);

var str = JSON.stringify(obj);
console.log(str); // 控制台返回 {"key":"value","jian":"zhi"}
```

## json字符数组转化为json数组

```js
var arrStr = '[{"name": "tom", "age": "18"}, {"name": "zhangsan", "age": "20"}]';
var arrObj = JSON.parse(arrStr);

console.log(arrObj); // 控制台返回 [{"name": "tom", "age": "18"}, {"name": "zhangsan", "age": "20"}]
console.log(arrObj[0]); // 控制台返回 {name: "tom", age: "18"}
console.log(arrObj[0].name); // 控制台返回 tom
console.log(arrObj[1].age); // 控制台返回 20
```

对于 json 数组，可以通过下标来进行访问。由于它是一个数组，所以也可以通过 for 循环进行遍历。