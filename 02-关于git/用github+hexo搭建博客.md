---
title: 用github+hexo搭建博客
toc: true
date: 2017-01-30 22:44:59
tags: git
---

  2016年月底第一次正式开始搭建博客，在学长和另一个小伙伴的帮助下，我初次认识github+hexo，被它给吸引。寒假开始后，就在准备换主题，因为我对原始主题实在无爱，强迫症越来越严重的我，不换好主题坚持不做笔记（无奈脸）。刚刚换好主题的我，觉得之前自己用了好几个晚上都没有换好主题的自己简直是傻bi（给自己一个黑人问号），不过好在自己现在换好了主题，赶紧做笔记，谨防自己忘了。

<!--more-->

## 清除，生成，部署 
```bash
$ hexo clean  or(hexo c)
$ hexo generate
$ hexo deploy
```

谨记：每次更改了一些信息后都要用这三步进行部署

## 安装yilia主题
```bash
$ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
```

安装好后，在_config.yml下修改theme：landscape为theme：yilia

## 写文章
1. 找到blog ☞ sources ☞ _post ☞ 写博客
2. 博客开头格式(以下为例子)：
`title: xxx`
`data: xxxx-xx-xx`
`tags: xxxx`
3. 如果文章较长，如果全都在主页显示，就会很累赘，浏览也不是很方便，那么就可以在每篇文章中加入```<!--more-->``` 

4. 文章写好直接执行下面命令即可直接发布文章
`$ hexo d -g`

## 注意

1.常用命令：

hexo new "post name" （新建文章）

hexo help （查看帮助）

hexo version （查看hexo的版本）

2.Markdown语法参考链接： [链接](https://www.zybuluo.com/mdeditor)


● [Hexo主题Yilia](http://litten.me/2014/08/31/hexo-theme-yilia/)



