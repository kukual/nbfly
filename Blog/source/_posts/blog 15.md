---
title: butterfly主题魔改12：留言板页面美化
categories: 博客搭建
tags:
  - hexo
  - butterfly
description: >-
  如果你希望为你的博客增添一个独特的留言板页面，这篇文章将是你不可或缺的指南。通过安装  hexo-butterfly-envelope 
  插件并进行简单的配置，你可以轻松创建一个充满创意的留言板页面。文章详细介绍了如何自定义留言板的样式，包括信笺头部图片、信封样式以及提示信息等，让你的留言板成为访客互动的亮点。
top_img: /img/129.jpeg
cover: /img/130.jpg
abbrlink: 6602dcbb
date: 2025-04-11 04:52:00
updated: 2025-04-11 04:52:00
swiper_index:
---
# butterfly主题魔改12：留言板页面美化
## 效果图
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509161144415.gif?imageSlim)
## 01 安装插件
输入以下命令：
```bash
npm install hexo-butterfly-envelope --save
```
## 02 修改配置文件
在博客根目录的`_config.butterfly.yml`文件后添加以下代码：
```yaml
# envelope_comment
# see https://akilar.top/posts/e2d3c450/
envelope_comment:
  enable: true #控制开关
  custom_pic:      
    cover: https://npm.elemecdn.com/hexo-butterfly-envelope/lib/violet.jpg #信笺头部图片
    line: https://npm.elemecdn.com/hexo-butterfly-envelope/lib/line.png #信笺底部图片
    beforeimg: https://npm.elemecdn.com/hexo-butterfly-envelope/lib/before.png # 信封前半部分
    afterimg: https://npm.elemecdn.com/hexo-butterfly-envelope/lib/after.png # 信封后半部分
  message: #信笺正文，多行文本，写法如下
    - 有什么想问的？
    - 有什么想说的？
    - 有什么想吐槽的？
    - 哪怕是有什么想吃的，都可以告诉我哦~
  bottom: 自动书记人偶竭诚为您服务！ #仅支持单行文本
  height: #1050px，信封划出的高度
  path: #【可选】comments 的路径名称。默认为 comments，生成的页面为 comments/index.html
  front_matter: #【可选】comments页面的 front_matter 配置
    title: 留言板
    comments: true
```


