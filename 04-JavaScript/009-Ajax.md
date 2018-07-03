AJAX，异步的 Javscript 和 XML，用于异步的获取服务器的数据。不需要刷新窗口，而获取服务器数据的一门技术。

## Ajax

> 1. 创建对象实例并初始化对象

```js
function createXMLHttpRequest() {
  if(window.XMLHttpRequest) {
    return new XMLHttpRequest();
  } else {
    // IE
    return new ActiveXObject('Microsoft.XMLHTTP');
  }
}
```

> 2. 指定响应处理函数

```js
var xhr = createXMLHttpRequest();
xhr.onreadystatechange = function() {
  if(xhr.readState == 4) {
    console.log('get response');
  }
};
```

`readyState` 有 5 种可能的取值：

* 0 (uninitialized, 未初始化)：对象已经创建但还没有调用 `open()` 方法。
* 1 (loading, 载入中)：`open()` 方法已经调用但请求还没有发送。
* 2 (loaded, 已载入)：请求已经发送。
* 3 (interactive, 交互中)：已经接收到部分响应。
* 4 (complete, 完成)：所有数据都已经收到，连接已经关闭。

> 3. 发出 http 请求

```js
var xhr = createXMLHttpRequest();
xhr.onreadystatechange = function() {
  if(xhr.readState == 4) {
    console.log('get response');
  }
};

xhr.send(null);
```

需要注意的是，`send()` 方法只接收一个参数，即表示请求主体的字符串。如果请求不包含主体（如：GET 请求就不包含主体），则必须传入 null。

> 4. 处理服务器返回的信息

`responseText` 或 `responseXML` 属性可以获得从请求返回的数据。

`responseText` 返回一个包含响应主体的字符串。

`responseXML` 返回一个 XML 文档对象，它仅当返回的内容类型为 `text/xml` 时才使用，并可以用 DOM 来处理。