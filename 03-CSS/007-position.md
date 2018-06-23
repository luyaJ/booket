`position` 属性用于指定一个元素在文档中的定位方式。`top`，`right`，`bottom` 和 `left` 属性则决定了该元素的最终位置。

position 的取值有：

* static：
  * 默认值，没有定位，元素正常出现在文档流中。
  * 对 `top`、`bottom`、`left`、`right` 和 `z-index` 属性无效。
* relative：
  * 生成相对定位的元素，相对于其正常位置进行定位。
  * 会在此元素未添加定位时所在位置留下空白。
  * 对 `table-*-group`、`table-row`、`table-column`、`table-cell`、`table-caption` 元素无效。
* absolute：
  * 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。
  * 不为元素预留空间。
* fixed：
  * 生成绝对定位的元素，相对于浏览器窗口进行定位。
  * 不为元素预留空间。

下面我们进行代码演示，初始代码如下，之后只写新增的代码：

```html
<div class="container">
  <div class="box"></div>
  <div class="box box_test"></div>
  <div class="box"></div>
</div>
```

```css
.box {
  height: 100px;
  width: 100px;
  border: 5px solid rgb(0, 0, 205);
  background: rgb(204, 204, 255);
  float: left;
  margin: 10px;
}

.box_test {
  border: 5px solid red;
  background: yellow;
}
```

> 1. static 元素正常出现在文档流中

```css
.box_test {
  position: static;
}
```

![position_static](http://p83c9hkzc.bkt.clouddn.com/position_static.png)

> 2. relative 元素相对于其正常位置进行定位

```css
.box_test {
  position: relative;
  top: 15px;
  left: 15px;
}
```

![position_relative](http://p83c9hkzc.bkt.clouddn.com/position_relative.png)

> 3. absolute 元素相对于非 static 定位的第一个父级元素进行定位

```css
.box_test {
  position: absolute;
  top: 25px;
  left: 25px;
}
```

![position_absolute](http://p83c9hkzc.bkt.clouddn.com/position_absolute.png)

> 4. fixed 元素相对于浏览器窗口进行定位

```css
.box_test {
  position: fixed;
  top: 35px;
  left: 35px;
}
```

![position_fixed](http://p83c9hkzc.bkt.clouddn.com/position_fixed.png)

资料：

* [MDN-position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)