我记得在《指尖上行》这本书中，`viewport` 讲的还是挺详细的。

移动设备上的 viewport 就是设备的屏幕上能用来显示我们的网页的那一块区域。

在移动端浏览器中以及某些桌面浏览器中，window对象有一个 `devicePixelRatio` 属性，它的官方的定义为：设备物理像素和设备独立像素的比例，也就是 `devicePixelRatio = 物理像素 / 独立像素`。

例如，在 Retina 屏的 iphone 上，devicePixelRatio 的值为2，也就是说1个 css 像素相当于2个物理像素。

```bash
<meta name="viewport" content="width=device-width,initial-scale=1.0,
minimum-scale=1.0,maximum-scale=1.0,user-scalable=no" />
```

1. width -- 设置viewport宽度，为一个正整数，或字符串‘device-width’
2. device-width -- 设备宽度
3. height -- 设置viewport高度，一般设置了宽度，会自动解析出高度，可以不用设置
4. initial-scale -- 默认缩放比例（初始缩放比例），为一个数字，可以带小数
5. minimum-scale -- 允许用户最小缩放比例，为一个数字，可以带小数
6. maximum-scale -- 允许用户最大缩放比例，为一个数字，可以带小数
7. user-scalable -- 是否允许手动缩放

这里提一个问题：
> 怎么处理移动端 1px 被渲染成 2px 问题

1 局部处理<br>
    mate标签中的 viewport 属性 ，initial-scale 设置为 1 
    rem 按照设计稿标准走，外加利用transfrome 的scale(0.5) 缩小一倍即可；

2 全局处理<br>
    mate标签中的 viewport 属性 ，initial-scale 设置为 0.5
    rem 按照设计稿标准走即可