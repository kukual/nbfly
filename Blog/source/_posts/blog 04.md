---
title: butterfly主题魔改01：准备工作及魔改流程目录
categories: 博客搭建
tags:
  - butterfly
  - hexo
description: 作为魔改系列的开篇，指导用户完成Butterfly主题的基础配置：包括主题安装、配置文件迁移（_config.butterfly.yml）、图片目录创建。同时列出后续12篇教程的目录，涵盖颜色、导航栏、动态背景、页面美化等主题，形成完整的定制路线图。强调通过分离配置文件避免版本冲突，为后续高阶修改奠定基础。
top_img: /img/105.jpeg
cover: /img/106.jpeg
abbrlink: 8ac25d20
date: 2025-03-31 04:52:00
updated: 2025-03-31 04:52:00
swiper_index: 4
---
# butterfly主题魔改01：准备工作及魔改流程目录
前面三篇文章分别是：
利用Github和hexo搭建自己的个人博客： https://kukual.github.io/posts/ec335aec/
腾讯云COS+Obsidian实现图片自动上传到图床： https://kukual.github.io/posts/77f87ebd/
hexo butterfly主题整体结构解析： https://kukual.github.io/posts/8ac25d19/
## 01 安装butterfly
在博客的根目录下打开bash键入以下命令：
```bash
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
npm install hexo-renderer-pug hexo-renderer-stylus --save
```
## 02 配置文件
1、修改博客的根目录下 `_config.yml` 中的 `theme` 属性为 `butterfly`
2、把博客的根目录下`themes\butterfly\_config.yml`复制一份重命名为`_config.butterfly.yml`，再移动到博客的根目录下。
## 03 设置一个图片存储目录
在博客的根目录的`source`目录下新建一个`img`文件夹，用于存储后续展示用的相关图片。
## 04 butterfly魔改流程目录
01：准备工作及魔改流程目录 https://kukual.github.io/posts/8ac25d20/
02：主题颜色、宽度设置、图片设置、遮罩效果 https://kukual.github.io/posts/8c39ed99/
03：导航栏设置（标题、菜单、搜索按钮） https://kukual.github.io/posts/4cb43628/
04：页面鼠标魔改-紫色水晶月光 https://kukual.github.io/posts/9ad33db7/
05：页面增加樱花动态背景效果 https://kukual.github.io/posts/1361a6d9/
06：首页页面美化 https://kukual.github.io/posts/a3208a35/
07：其他设置 https://kukual.github.io/posts/b9aac97d/
08：侧边栏及其卡片美化、文章等页面渐变背景 https://kukual.github.io/posts/ab8ee243/
09：页脚美化和右下角按钮设置 https://kukual.github.io/posts/aa370e8f/
10：分类页面魔改 https://kukual.github.io/posts/a7bebfb0/
11：文章页面美化 https://kukual.github.io/posts/4c242966/
12：留言板页面美化 https://kukual.github.io/posts/6602dcbb/
13：关于页面美化（手搓） https://kukual.github.io/posts/4be26d1b/


