---
title: toLocaleString
date: 2018-04-05 23:06:21
---

今天看到的一篇文章，记录下，并动手实践。

`toLocaleString` 方法是用于返回格式化对象后的字符串，这个字符串因不同语言而不同，可以通过传参决定。语法：
```bash
object.toLocaleString([locales [, options]]);
```

`locales` 参数用于指定格式化对象时使用的语言环境（不区分大小写），默认为当前环境的语言，可以不传。
```bash
const date = new Date();
date.toLocaleString();       // 2018/4/5 下午11:25:19
date.toLocaleString('zh');   // 2018/4/5 下午11:25:19
date.toLocaleString('en');   // 4/5/2018, 11:25:19 PM   
```

# Date.prototype.toLocaleString

参考：[MDN中的Date.prototype.toLocaleString](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString)

hour12 表示是使用十二小时制还是二十四小时制，默认值视 `locales` 而定。例子如下：
```bash
const date = new Date();
date.toLocaleString('zh', { hour12: true });        // 2018/4/6 上午12:04:18
date.toLocaleString('zh', { hour12: false });       // 2018/4/6 00:04:18
```

# Number.prototype.toLocaleString

> 如何去格式化数字，使整数部分每三位加一个逗号

一般我们会去用正则，但是最快的方式是使用`toLocaleString`。
```bash
const num = 66666666;
num.toLocaleString();  //66,666,666 
```

参考：[MDN中的Number.prototype.toLocaleString](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString)

我们再来讲一讲`options`参数：

1.`style`
格式化时使用的样式，可能的值有“decimal”表示纯数字格式，“currency”表示货币格式，"percent"表示百分比格式。默认值是 "decimal"。

```bash
const num = 66666666;
num.toLocaleString('zh', {style: 'decimal'});    // 66,666,666
num.toLocaleString('zh', {style: 'percent'});    // 6,666,666,600%
num.toLocaleString('zh', {style: 'currency'});   // Uncaught TypeError: Currency code is required with currency style.
```

2.`currency`
在货币格式化中使用的货币符号。可能的值是ISO的货币代码，无默认值。例如"USD" 表示美元，"EUR" 表示欧元，or "CNY"是人民币。在上面的例子中，第三个报错了。这是因为一定要提供货币属性。
```bash
const num = 66666666;
num.toLocaleString('zh', {style: 'currency', currency: 'CNY'});     // ￥66,666,666.00
num.toLocaleString('zh', { style: 'currency', currency: 'cny', currencyDisplay: 'name' });   // 66,666,666.00人民币
```

---

学习资料：[想偷懒的话，toLocaleString 了解一下？](https://juejin.im/post/5ac472016fb9a028c22afa9d?utm_source=gold_browser_extension)