我们设置 5 个按钮：

```html
<button>点击</button>
<button>点击</button>
<button>点击</button>
<button>点击</button>
<button>点击</button>
```

接着看以下代码：

```js
var button = document.querySelectorAll('button');

for(var i = 0; i < button.length; i++) {
  button[i].onclick = 
    e => console.log('点击了第 ' + i + '个按钮');
}
```

想想看，当你点击按钮时，会打印出什么样的结果？

我们会在控制台发现，不论点击哪个按钮，出现的结果都是 *点击了第 5个按钮*。

那么，我们如何解决这个问题呢？

最简单的方法当然就是将 `var` 替换成 `let`：

```js
var button = document.querySelectorAll('button');

for(let i = 0; i < button.length; i++) {
  button[i].onclick = 
    e => console.log('点击了第 ' + i + '个按钮');
}

<!-- 依次点击5个按钮 控制台结果显示如下 -->
// 点击了第 0个按钮
// 点击了第 1个按钮
// 点击了第 2个按钮
// 点击了第 3个按钮
// 点击了第 4个按钮
```

再想想，还有什么办法吗？

嗯...那就用闭包吧！

```js
var button = document.querySelectorAll('button');

for(let i = 0; i < button.length; i++) {
  (function(i) {
    button[i].onclick = 
      e => console.log('点击了第 ' + i + '个按钮');
  })(i);
}
```

输出的结果和使用 `let` 的方法相同。