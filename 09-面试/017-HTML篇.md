# 浏览器页面有哪三层构成，分别是什么，作用是什么?

构成：结构层、表示层、行为层

分别是：HTML (HyperText Makeup Language 超文本标记语言)、CSS (Cascading Style Sheets 层叠样式表)、JavaScript。

作用：HTML 实现页面的结构、CSS 完成页面的表现与风格、JavaScript 实现一些客户端的功能与业务。

# Doctype作用?

Doctype 即 Document Type，位于文档中的最前面，处于标签之前。用来告知浏览器解析器，用什么文档类型来规范解析这个文档。是 HTML 中用来区分标准模式和怪异模式的声明。

* 标准模式：使用 `<!DOCTYPE html>`，按照浏览器的 HTML 和 CSS 标准来对文档进行解析和渲染。
* 怪异模式：使用浏览器自己的方式解析执行代码。

# 对WEB标准以及W3C的理解与认识?

1. 文档顶部使用 `<!DOCTYPE html>` 
2. 标签用小写（ul、div）
3. 标签之间不乱嵌套
4. meta、link、input 等标签尾部不需要加 `/`
5. 提高搜索机器人的搜索几率
6. 使用外链 css 和 js 脚本
7. 结构行为表现的分离
8. 文件下载和页面速度更快、内容能被更多的用户和更广泛的设备所访问
9. 更少的代码和组件，容易维护、改版方便，不需要变动页面内容

# HTML5的优点、缺点以及有哪些新特性? 说说你对HTML5的认识?

> 优点：

* 网站标准统一、HTML5 本身是由 W3C 推荐出来的；
* 多设备、跨平台；
* 及时更新；
* 提高可用性和改进用户的友好体验； 
* 增加了新的标签，有助于开发人员定义重要的内容；
* 可以给站点带来更多的多媒体元素（视频和音频）；
* 可以很好的替代 flash 和 silverlight；
* 涉及到网站的抓取和索引的时候，多于 SEO 很友好；
* 被大量应用于移动应用程序和游戏。

> 缺点：

* 安全：web storage、web socket 这样的功能很容易被黑客利用，来盗取用户的信息和资料；
* 兼容性：IE9 以下的浏览器几乎全军覆没；
* 完善性：许多特性各个浏览器的支持程度不一样；
* 技术门槛：需要学习 API，像 web storage、web worker 等，后台甚至需要浏览器原理的知识；
* 性能：某些平台上的引擎问题导致 HTML5 性能低下。

> 新特性：

header、footer、article、section、nav、aside、figure、code、dialog、figure、meter、time、progress、video、audio、details。

> 认识：

HTML5 指的是 HTML、CSS 和 JavaScript 在内的一套技术组合，它希望能够减少网页浏览器对于需要插件的丰富性网络应用服务。增强了浏览器的原生功能，减少了 Web 应用对插件的依赖，让用户体验更好，让开发更加方便。

# 你做的网页在哪些浏览器测试过，这些浏览器的内核分别是什么?

1. IE：trident 内核
2. Firefox：gecko 内核
3. Safari：webkit 内核
4. Opera：Google Chrome 的 Blink 内核
5. Chrome：Blink（基于 webkit）

# HTML5行内元素有哪些，块级元素有哪些，空元素有哪些?

> 行内元素：a、img、input、label、select、span。

又称内联元素，不独占区域，大小仅仅依赖于自身内容的大小（例如文字和图片），常用于控制页面中文本样式。

特点：和相邻的元素在同一行上；设置宽高无效，水平方向 margin、padding 可设，垂直方向无效；行内元素只可以容纳其他行内元素或文本。

> 块级元素：div、p、ol、ul、dl、form、table、h1-h6

独占一行或多行，可以设置宽高。

特点：总是另起一行；在不设宽的情况下，默认占所在容器宽度的100%；可以容纳行内元素和其他的块元素；文字类的块元素不可以放块元素。

> 空元素 (没有内容的 HTML 元素被称为空元素)：`<br/>`、`<hr>`、`<input>`、`<img>`、`<link>`、`<meta>`

# 请你描述一下 cookies，sessionStorage 和 localStorage 的区别?

> 区别：①容量 ②是否会携带到 ajax 中（cookie 每次都会，而另两个不会，只做存储）③API 易用性

sessionStorage 和 localStorage 是 HTML5 Web Storage API 提供的，可以在 web 请求之间保存数据，有了本地数据，就可以避免数据在浏览器和服务器间不必要地来回传递。

cookies，sessionStorage 和 localStorage 都是在浏览器端存储数据的。

cookies 用于客户端与服务端之间的通信，但它有本地存储的功能。缺点就是：每个域名存储量太小，只有 4KB；会随请求发送给服务器，影响获取资源的效率。

localStorage 最大容量为 5MB，永久存储。

sessionStorage 只在 session 中有效，只要浏览器窗口没有关闭，数据就仍然存在。关闭窗口后，sessionStorage 就被销毁。

三者的作用域不同，sessionStorage 不在不同的浏览器窗口中共享，即使是同一个页面；localStorage 在所有同源窗口中都是共享的；cookie 也是在所有同源窗口中都是共享的。

# 说说你对HTML语义化的理解?

> 什么是 HTML 语义化？

根据内容的结构化，选择合适的标签（代码语义化）便于开发者阅读和写出更加优雅的代码同时让浏览器的爬虫和机器更好的解析。

> 为什么语义化？

* 裸奔时好看：为了在没有 CSS 的情况下，页面也能呈现出很好的内容结构、代码结构；
* 用户体验：例如 title、alt 用于解释名词或图片信息，label 标签的活用；
* 有利于 SEO：和搜索引擎建立良好的沟通，有助于爬虫抓取更多的有效信息；
* 便于团队开发和维护，语义化更具可读性。

# link和@import的区别?

两个都是外部引用 CSS 的方式，但是存在一定的区别：

1. `link` 是 XHTML 标签，除了加载 CSS 外，还可以定义 RSS 等其他事务；`@import` 属于 CSS 范畴，只能加载 CSS。
2. `link` 引用 CSS 时，在页面载入时同时加载；`@import` 需要等页面网页完全载入后再加载。
3. `link` 是 XHTML 标签，无兼容性问题；`@import` 是在 CSS2.1 提出的，低版本的浏览器不支持。
4. `link` 支持使用 JavaScript 控制 DOM 去改变样式；而 `@import` 不支持。

# data- 属性的作用是什么？

`data-` 是 HTML5 中新增的为前端开发者提供的自定义属性，这些属性值可以通过对象的 `dataset` 属性获取，不支持该属性的浏览器可以通过 `getAttribute` 方法获取。

当没有合适的属性和元素时，自定义的 data 属性能够存储页面或 App 的私有自定义数据。