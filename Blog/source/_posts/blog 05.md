---
title: butterfly主题魔改02：主题颜色、宽度设置、图片设置、遮罩效果
categories: 博客搭建
tags:
  - butterfly
  - hexo
description: 聚焦视觉层初级定制，通过修改_config.butterfly.yml实现深紫色系主题配色，调整页面最大宽度为70%。详细说明各类图片配置（头像、背景、封面、404页），并关闭页头/页脚的半透明遮罩效果。提供完整的YAML代码段和Stylus样式示例，适合用户快速统一博客视觉风格，提升页面简洁度与加载性能。
top_img: /img/109.jpg
cover:  /img/110.jpg
abbrlink: 8c39ed99
date: 2025-04-01 04:52:00
updated: 2025-04-01 04:52:00
swiper_index:
---
# butterfly主题魔改02：主题颜色、宽度设置、图片设置、遮罩效果
## 01 修改主题颜色：深紫色系
根目录下`_config.butterfly.yml`文件`theme_color`设置
```yaml
theme_color:
  enable: true                # 启用主题颜色自定义
  main: "#6a0dad"            # 主色调 - 深紫色（用于导航栏等主要UI元素）
  paginator: "#9b30ff"       # 分页器颜色 - 明亮的紫罗兰色（分页按钮颜色）
  button_hover: "#9932cc"    # 按钮悬停色 - 深兰花紫（按钮鼠标悬停效果色）
  text_selection: "#9370db"  # 文本选中背景色 - 中紫色（选中文字时的背景色）
  link_color: "#8a2be2"      # 超链接颜色 - 蓝紫色（文章内链接颜色）
  meta_color: "#9370db"      # 元信息文字色 - 中紫色（作者、日期等元信息颜色）
  hr_color: "#9932cc"        # 水平线颜色 - 深兰花紫（分隔线颜色）
  code_foreground: "#4b0082" # 代码文字色 - 靛青色（代码块文字颜色）
  code_background: "rgba(106, 13, 173, 0.05)" # 代码块背景 - 深紫色极淡透明（代码块背景色）
  toc_color: "#8a2be2"       # 目录文字色 - 蓝紫色（文章目录文字颜色）
  blockquote_padding_color: "#6a0dad" # 引用框边框色 - 深紫色（引用框左侧边框色）
  blockquote_background_color: "#6a0dad" # 引用框背景 - 深紫色（引用框背景色）
  scrollbar_color: "#6a0dad" # 滚动条颜色 - 深紫色（页面滚动条颜色）
  meta_theme_color_light: "#f5f0fa" # 浅色模式主题色 - 淡紫色（浏览器主题色-浅色模式）
  meta_theme_color_dark: "#2d0a3d"  # 深色模式主题色 - 暗紫色（浏览器主题色-深色模式）
```
## 02 页面宽度设置
根目录下`themes\butterfly\source\css\_page\common.styl`文件`.layout`部分
```styl
// 主布局容器
.layout
  display: flex
  flex: 1 auto           // 自动填充剩余空间
  margin: 0 auto         // 水平居中
  padding: 40px 15px     // 内边距
  max-width: 70%      // 最大宽度
  width: 100%            // 默认100%宽度
```
## 03 各种图片设置（背景，头像，封面等等）
博客根目录下`_config.butterfly.yml`文件的`图片设置`的代码如下：
```yaml
# --------------------------------------
# 图片设置
# --------------------------------------
favicon: /img/01.png # 网站图标（favicon）
# 头像设置
avatar:
  img: /img/02.jpg  # 头像图片路径
  effect: true     # 是否启用头像特效（如旋转等）
disable_top_img: false # 是否禁用所有顶部横幅图片
default_top_img: rgba(0, 0, 0, 0) # 当页面未设置横幅图片时显示的默认背景（此处设置为透明）
index_img: # 首页横幅图片（留空则使用默认）
archive_img: # 归档页横幅图片（留空则使用默认）
tag_img: # 标签页横幅图片（注意：单个标签页，非标签集合页）
tag_per_img: # 为特定标签设置独立横幅图片
# 格式：
#  - 标签名: 图片路径
category_img: # 分类页横幅图片（注意：单个分类页，非分类集合页）
category_per_img: # 为特定分类设置独立横幅图片
# 格式：
#  - 分类名: 图片路径
footer_img: rgba(45, 10, 61, 0.2)  # 页脚背景图片（true表示启用主题默认，也可指定路径）
background: /img/03.png # 网站背景（支持颜色值或图片路径）
# 封面图片设置
cover:
  index_enable: true  # 首页是否启用封面
  aside_enable: true  # 侧边栏是否启用封面
  archives_enable: true  # 归档页是否启用封面
  default_cover: /img/04.png  # 默认封面图片（当未设置封面时使用）
# 图片加载失败时的替代图片
error_img:
  flink: /img/05.jpg      # 友链页面错误图片
  post_page: /img/06.jpg  # 文章页面错误图片
# 404页面设置
error_404:
  enable: true            # 是否启用自定义404页面
  subtitle: '页面不存在'   # 404提示文字
  background: /img/07.png  # 404背景图片
# Instant.page 预加载技术
# https://instant.page/
instantpage: false  # 是否启用页面预加载
# 图片懒加载配置
# https://github.com/verlok/vanilla-lazyload
lazyload:
  enable: false  # 是否启用懒加载
  # 指定应用懒加载的范围（全站 site 或仅文章 post）
  field: site
  placeholder:  # 懒加载占位图路径
  blur: false   # 是否启用模糊效果
```
## 04 关闭页头和页脚的遮罩效果
博客根目录下`_config.butterfly.yml`文件的`页头和页脚的遮罩效果`部分
```yaml
# 页头和页脚的遮罩效果
mask:
  header: false                  # 页头遮罩
  footer: false                  # 页脚遮罩
```






