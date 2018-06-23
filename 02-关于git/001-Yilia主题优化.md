---
title: Yilia主题优化
date: 2017-07-15 17:56:56
tags: git
toc: true
---

过了大半年，该是要好好整理下自己的博客了。

<!--more-->

## github+hexo

### 新建文章：

	$ hexo new "新的文章"

然后你就发现blog根目录下的source文件夹中的_post文件夹中多了一个 **新的文章.md** 文件

### 本地服务预览：

	$ hexo s  //server  （会监视文件变动并自动更新）

觉得自己的文章没问题后，就通过`hexo g` , `hexo d`生成和部署网页

### 清除缓存：

	$ hexo clean

### 生成：

	$ hexo g  //generate

### 部署：

	$ hexo d  //deploy

上面两部可以合起来

	$ hexo d -g

**[hexo所有主题传送门](https://hexo.io/themes/)**

**[markdown语法](https://maxiang.io/)**

**[markdownPad下载](http://www.markdownpad.com/)**

推荐几个我觉得不错的主题：

- [Ochuuunn](http://ochukai.me/) /  [github下载](https://github.com/ochukai/hexo-theme-ochuunn)
- [Random](http://hexo-theme-random.herokuapp.com/) / [github下载](https://github.com/stiekel/hexo-theme-random)

## 安装主题

	$ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia

### 配置

修改hexo根目录下的`_config.yml` ： `theme : yilia`

### 更新

	$ cd themes/yilia
	$ git pull

上面是老东西，下面是优化

## 添加文章目录

### 添加css样式

打开`themes\yilia\source`下的 `main.2d7529.css`文件(这里好像名字会不一样，没关系，找到.css文件就ok了)，在里面添加代码：

	/* 新添加的 */
	#container .show-toc-btn,#container .toc-article{display:block}
	.toc-article{z-index:100;background:#fff;border:1px solid #ccc;max-width:250px;min-width:150px;max-height:500px;overflow-y:auto;-webkit-box-shadow:5px 5px 2px #ccc;box-shadow:5px 5px 2px #ccc;font-size:12px;padding:10px;position:fixed;right:35px;top:129px}.toc-article .toc-close{font-weight:700;font-size:20px;cursor:pointer;float:right;color:#ccc}.toc-article .toc-close:hover{color:#000}.toc-article .toc{font-size:12px;padding:0;line-height:20px}.toc-article .toc .toc-number{color:#333}.toc-article .toc .toc-text:hover{text-decoration:underline;color:#2a6496}.toc-article li{list-style-type:none}.toc-article .toc-level-1{margin:4px 0}.toc-article .toc-child{}@-moz-keyframes cd-bounce-1{0%{opacity:0;-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}60%{opacity:1;-o-transform:scale(1.01);-webkit-transform:scale(1.01);-moz-transform:scale(1.01);-ms-transform:scale(1.01);transform:scale(1.01)}100%{-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}}@-webkit-keyframes cd-bounce-1{0%{opacity:0;-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}60%{opacity:1;-o-transform:scale(1.01);-webkit-transform:scale(1.01);-moz-transform:scale(1.01);-ms-transform:scale(1.01);transform:scale(1.01)}100%{-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}}@-o-keyframes cd-bounce-1{0%{opacity:0;-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}60%{opacity:1;-o-transform:scale(1.01);-webkit-transform:scale(1.01);-moz-transform:scale(1.01);-ms-transform:scale(1.01);transform:scale(1.01)}100%{-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}}@keyframes cd-bounce-1{0%{opacity:0;-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}60%{opacity:1;-o-transform:scale(1.01);-webkit-transform:scale(1.01);-moz-transform:scale(1.01);-ms-transform:scale(1.01);transform:scale(1.01)}100%{-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}}.show-toc-btn{display:none;z-index:10;width:30px;min-height:14px;overflow:hidden;padding:4px 6px 8px 5px;border:1px solid #ddd;border-right:none;position:fixed;right:40px;text-align:center;background-color:#f9f9f9}.show-toc-btn .btn-bg{margin-top:2px;display:block;width:16px;height:14px;background:url(http://7xtawy.com1.z0.glb.clouddn.com/show.png) no-repeat;-webkit-background-size:100%;-moz-background-size:100%;background-size:100%}.show-toc-btn .btn-text{color:#999;font-size:12px}.show-toc-btn:hover{cursor:pointer}.show-toc-btn:hover .btn-bg{background-position:0 -16px}.show-toc-btn:hover .btn-text{font-size:12px;color:#ea8010}
	.toc-article li ol, .toc-article li ul { margin-left: 30px; } .toc-article ol, .toc-article ul { 
	margin: 10px 0; }

### 修改article.ejs文件

打开`themes\yilia\layout\_partial`文件夹下的`article.ejs`文件，在`</header> <% } %` 下面加入如下内容(注意插入的位置):

	<!-- 目录内容 -->
    <% if (!index && post.toc){ %>
    <p class="show-toc-btn" id="show-toc-btn" onclick="showToc();" style="display:none">
      <span class="btn-bg"></span>
      <span class="btn-text">文章导航</span>
    </p>
    <div id="toc-article" class="toc-article">
      <span id="toc-close" class="toc-close" title="隐藏导航" onclick="showBtn();">×</span>
      <strong class="toc-title">文章目录</strong>
      <%- toc(post.content) %>
    </div>
    <script type="text/javascript">
      function showToc(){
        var toc_article = document.getElementById("toc-article");
        var show_toc_btn = document.getElementById("show-toc-btn");
        toc_article.setAttribute("style","display:block");
        show_toc_btn.setAttribute("style","display:none");
      };
      function showBtn(){
        var toc_article = document.getElementById("toc-article");
        var show_toc_btn = document.getElementById("show-toc-btn");
        toc_article.setAttribute("style","display:none");
        show_toc_btn.setAttribute("style","display:block");
      };
    </script>
    <% } %>
    <!-- 目录内容结束 -->

**如果想要文章显示目录，要在每篇文章的开头加入：`toc: true`**
	
![目录效果图](http://ot4r4qnml.bkt.clouddn.com/catalogue.PNG)

## 添加其他一些东西

### 添加“关于”

	$ hexo new page "about"

此时，`source`中就会多出一个文件夹，名为`about`,可以在里面编辑内容

在`themes/yilia/_config.yml`添加下面内容：

	menu:
		关于: /about

### 添加RSS

	$ npm install hexo-generator-feed --save

注意完整的输入上面的代码，`--save`不能省，否则插件信息不能写入package.json，之后`hexo clean` 、`hexo g`,查看public文件夹，里面多了一个atom.xml文件夹表示成功。

### 添加sitemap

	$ npm install hexo-generator-sitemap --save

`hexo clean` 、`hexo g`,查看public文件夹，可以看到sitemap.xml文件。

sitemap的初衷是给搜索引擎看的，为了提高搜索引擎对自己站点的收录效果，我们最好手动到google和百度等搜索引擎提交sitemap.xml。

### 添加本站访问次数

在`themes/yilia/layout/_partial` 下找到footer.ejs , 在里面加入以下代码：

	<script async src="//dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>

	<span id="busuanzi_container_page_pv">
		本文总阅读量<span id="busuanzi_value_page_pv"></span>次
	</span>
	
### 文章模板

打开hexo/scaffolds/post.md , 可以看到：

	---
	title: {{ title }}
	date: {{ date }}
	tags:
	---

做以下的修改，每次自动生成目录：

	---
	title: {{ title }}
	date: {{ date }}
	tags:
	toc: true
	---
	
**注：** 如果想要多个tag，则以这样的格式显示`tages: [js,css]`

### 给网页加ico图标

1. 增加网站标题栏logo，很简单。将图片改成32*32格式的ico图标（这里我是在线转换的）
2. 在文件中找到`E:\blog\themes\yilia\layout\_partial`，再找到`head.ejs`,在里面增加语句`<link rel="shortcut icon" href="图片地址">`

**注意：** 如果把ico图标放在网站根目录下，那么浏览器会不停的搜索网站根目录。






