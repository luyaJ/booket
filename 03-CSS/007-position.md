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
* sticky：
  * 粘性定位，被认为是相对定位和固定定位的混合。元素在跨越特定的阈值前为相对定位，之后为固定定位。

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

![position_static](https://s2.ax1x.com/2019/03/02/kbXCTg.png)

> 2. relative 元素相对于其正常位置进行定位

```css
.box_test {
  position: relative;
  top: 15px;
  left: 15px;
}
```

![position_relative](https://s2.ax1x.com/2019/03/02/kbOzOf.png)

> 3. absolute 元素相对于非 static 定位的第一个父级元素进行定位

```css
.box_test {
  position: absolute;
  top: 15px;
  left: 15px;
}
```

![position_absolute](https://s2.ax1x.com/2019/03/02/kbOHTe.png)

> 4. fixed 元素相对于浏览器窗口进行定位

```css
.box_test {
  position: fixed;
  top: 15px;
  left: 15px;
}
```

> 5. sticky 元素在跨域某个阈值前为相对定位，之后为固定定位

```html
<div class="container">
  <dl>
    <dt>A</dt>
    <dd>Adrew. W.K</dd>
    <dd>ASDFF</dd>
    <dd>ARETYY</dd>
    <dd>AVFGHF</dd>
  </dl>
  <dl>
    <dt>C</dt>
    <dd>Chrome</dd>
    <dd>Common</dd>
    <dd>Converse</dd>
    <dd>Crystal Castles</dd>
    <dd>Cursive</dd>
  </dl>
  <dl>
    <dt>E</dt>
    <dd>Explosions In The Sky</dd>
  </dl>
  <dl>
    <dt>T</dt>
    <dd>Ted Leo & The Pharmacists</dd>
    <dd>T-Pain</dd>
    <dd>Thrice</dd>
    <dd>TV On The Radio</dd>
    <dd>Two Gallants</dd>
  </dl>
</div>
```

```css
* { 
  margin: 0;
  padding: 0;
  box-sizing: border-box; 
}
dl {
  margin: 0;
  padding: 24px 0 0 0;
}
dt {
  background: darkcyan;
  border-bottom: 1px solid #dddddd;
  border-top: 1px solid #717D85;
  color: #fff;
  font: bold 18px/21px Helvetica, Arial, sans-serif;
  margin: 0;
  padding: 2px 0 0 12px;
  position: -webkit-sticky;
  position: sticky;
  top: -1px;
}
dd {
  font: bold 20px/45px Helvetica;
  margin: 0;
  padding: 0 0 0 12px;
  white-space: nowrap;
}

dd + dd {
  border-top: 1px solid #CCC;
}
```

![position_sticky](https://s2.ax1x.com/2019/03/02/kbXK7F.png)

资料：

* [MDN-position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)