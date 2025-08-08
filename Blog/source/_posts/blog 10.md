---
title: butterfly主题魔改07：其他设置
categories: 博客搭建
tags:
  - hexo
  - butterfly
description: >-
  本文介绍了Butterfly主题的多项实用功能配置。首先，通过安装hexo-wordcount插件实现文章字数统计与阅读时长显示，支持在文章页和侧边栏展示数据。其次，优化复制功能，支持添加版权信息并设置字数阈值。文章元数据部分允许自定义首页和文章页的日期类型（创建/更新时间）、分类标签样式及显示位置。全局字体设置详细说明了如何调整字体大小、代码字体及在线字体的引入，确保页面视觉统一。最后，通过配置社交媒体链接，使用FontAwesome图标库添加GitHub、CSDN、小红书等平台链接，并自定义图标颜色，增强博客的交互性与品牌感。
top_img: /img/119.jpeg
cover: /img/120.jpeg
abbrlink: b9aac97d
date: 2025-04-06 04:52:00
updated: 2025-04-06 04:52:00
swiper_index:
---
# butterfly主题魔改07：其他设置
## 01 字数统计功能
安装插件。
```bash
npm install hexo-wordcount --save
```
博客根目录下`_config.butterfly.yml`文件的`字数统计功能设置`的代码如下：
```yaml
# 需要安装hexo-wordcount插件 
wordcount: 
  enable: true   # 是否启用字数统计功能 
  post_wordcount: true   # 是否在文章元数据中显示文章的字数统计 
  min2read: true   # 是否在文章元数据中显示阅读文章所需的时间 
  total_wordcount: true   # 是否在侧边栏的网站信息中显示网站的总字数统计
```
## 02 复制功能设置
博客根目录下`_config.butterfly.yml`文件的`复制功能设置`的代码如下：
```yaml
# 复制功能设置 
copy: 
  enable: true   # 是否启用复制功能 
  copyright:   # 是否在复制内容后添加版权信息 
    enable: true     # 是否启用版权信息添加功能 
    limit_count: 300     # 当复制的内容字数超过该限制时，才添加版权信息 
```
## 04 文章元数据显示设置
博客根目录下`_config.butterfly.yml`文件的`文章元数据显示设置`的代码如下：
```yaml
# --------------------------------------
# 文章元数据显示设置
# --------------------------------------
post_meta:
  # 首页设置
  page:
    date_type: created    # 显示日期类型：created（创建时间）/updated（更新时间）/both（两者）
    date_format: date     # 日期格式：date（完整日期）/relative（相对时间，如"2天前"）
    categories: true      # 是否显示分类
    tags: true           # 是否显示标签
    label: true           # 是否显示标签样式
  # 文章页设置
  post:
    position: center        # 元数据显示位置：left（左）/center（中）
    date_type: both       # 显示日期类型
    date_format: date     # 日期格式
    categories: true      # 是否显示分类
    tags: true            # 是否显示标签
    label: true           # 是否显示标签样式
```
## 05 全局字体设置
博客根目录下`_config.butterfly.yml`文件的`全局字体设置`的代码如下：
```yaml
# 全局字体设置
# 除非知道如何运作，否则不要修改以下设置
font:
  global_font_size: 17px  # 全局字体大小（例如：16px）
  code_font_size: 15px # 代码字体大小（例如：14px）
  font_family: "'Chewy', 'Ma Shan Zheng', cursive"  # 全局字体族（例如：'Helvetica Neue'）
  code_font_family: 'Consolas'  # 代码字体栈
    # 代码字体族（例如：'Consolas'）
# 网站标题字体设置
blog_title_font:
 # 在线字体链接（Google Fonts等）
  font_link: 'https://fonts.googleapis.com/css2?family=Chewy&family=Ma+Shan+Zheng&family=Fredoka+One&display=swap' 
  font_family: "'Fredoka One', 'Ma Shan Zheng', cursive"    # 字体族名称
```
## 06 社交媒体链接配置
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509160959939.png?imageSlim)
博客根目录下`_config.butterfly.yml`文件
```yaml
# --------------------------------------
# 社交媒体链接配置
# 格式：图标类名: 链接地址 || 显示文字 || 图标颜色
# 颜色值支持：十六进制码 / RGB / 颜色名称
# FontAwesome图标库：https://fontawesome.com/icons
# --------------------------------------
social:
  fab fa-github: https://github.com/kukual || Github || '#8a2be2'
  fa-solid fa-code: https://blog.csdn.net/weixin_74811095 || CSDN || '#8a2be2'
  fa-solid fa-book: https://www.xiaohongshu.com/user/profile/5e8a0aae0000000001002ce4 || redbook || '#8a2be2'
  fab fa-bilibili: https://space.bilibili.com/498478848 || bilibili || '#8a2be2'
  # 示例配置：
  # fab fa-github: https://github.com/用户名 || Github || '#24292e'
  # fas fa-envelope: mailto:邮箱地址 || 邮箱 || '#4a7dbe'
```



