---
title: butterfly主题魔改11：文章页面美化
categories: 博客搭建
tags:
  - hexo
  - butterfly
description: >-
  这篇文章详细介绍了如何通过Butterfly主题的魔改，提升文章页面的用户体验。从目录设置、版权声明到打赏功能和相关文章推荐，作者展示了如何通过配置文件的调整，让文章页面更加丰富和实用。同时，文章还探讨了代码块的美化、标题前缀图标以及分享系统的配置，帮助读者打造出一个既美观又功能强大的文章页面。无论你是技术博主还是创意写作者，这篇文章都将为你提供实用的美化技巧。
top_img: /img/127.jpeg
cover: /img/128.jpeg
abbrlink: 4c242966
date: 2025-04-10 04:52:00
updated: 2025-04-10 04:52:00
swiper_index:
---
# butterfly主题魔改11：文章页面美化
## 01 文章页面设置
修改目录设置、文章版权声明、打赏设置、相关文章推荐等板块。
博客根目录下`_config.butterfly.yml`文件的`文章页面设置`的代码如下：
```yaml
# --------------------------------------
# 文章页面设置
# --------------------------------------
# 目录设置
toc:
  post: true        # 在文章中显示目录
  page: true       # 在普通页面隐藏目录
  number: true      # 显示章节编号
  expand: false     # 是否默认展开所有目录层级
  style_simple: false  # 使用简约目录样式（true/false）
  scroll_percent: true  # 显示阅读进度百分比
# 文章版权声明
post_copyright:
  enable: true      # 启用版权信息显示
  decode: false     # 是否对作者信息进行解码（常用于中文转义）
  author_href: https://kukual.github.io/     # 作者主页链接（可选）
  license: CC BY-NC-SA 4.0  # 采用的协议名称
  license_url: https://creativecommons.org/licenses/by-nc-sa/4.0/  # 协议详情链接
# 打赏设置
reward:
  enable: true
  text: "感谢您的支持！" # 打赏提示文字
  comment: "请我喝杯咖啡吧~" # 打赏留言
  QR_code:  # 收款码配置
    - img: /img/wechat.jpg
      text: 微信
    # - img: /img/alipay.jpg
    #   link: 支付宝二维码链接
    #   text: 支付宝打赏
# 在线编辑按钮
post_edit:
  enable: false
  url:  # 代码仓库编辑路径（示例：https://github.com/用户名/仓库名/edit/分支名/）
# 相关文章推荐
related_post:
  enable: true
  limit: 6  # 显示数量
  # 关联依据: created（创建时间）/ updated（更新时间）
  date_type: created
# 文章分页方式
post_pagination: 1 # 1 - 旧文章在前 | 2 - 新文章在前 | false - 禁用分页
# 文章过期提示
noticeOutdate:
  enable: true
  style: flat  # 样式: simple（简洁）/ flat（扁平）
  limit_day: 365  # 触发天数（超过指定天数未更新显示提示）
  position: top  # 显示位置: top（顶部）/ bottom（底部）
  # 提示信息模板
  message_prev: 本文最后更新于
  message_next: 天前，部分内容可能已失效
```
## 02 代码块设置
效果图
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509161052704.png?imageSlim)
博客根目录下`_config.butterfly.yml`文件的`代码块设置`的代码如下：
```yaml
# --------------------------------------
# 代码块设置
# --------------------------------------
code_blocks:
  # 代码主题: darker（暗黑）/ pale night（浅夜）/ light（明亮）/ ocean（海洋）/ false（禁用）
  theme: darker
  macStyle: true # 是否显示Mac风格代码栏（带红黄绿按钮）
  height_limit: 400  # 代码块高度限制（单位：px，false表示不限制）
  word_wrap: true  # 是否自动换行
  # 工具栏设置
  copy: true  # 是否显示复制按钮
  language: true # 是否显示语言标签
  # 代码块显示方式: 
  #   true - 折叠代码块 | false - 展开代码块 | none - 展开代码块并隐藏折叠按钮
  shrink: false
  fullpage: true  # 是否显示全屏查看按钮
```
## 03 文章内容标题前缀图标
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509161052706.png?imageSlim)
博客根目录下`_config.butterfly.yml`文件的`文章内容美化配置`的代码如下：
```yaml
# 文章内容美化配置
beautify:
  enable: true                 # 是否启用内容美化
  field: post   # 应用范围：site (全站) / post (仅文章)                  
  title_prefix_icon: '\f0e7' # 标题前缀图标（使用Font Awesome的Unicode值，例如：'\f0c1'）
  title_prefix_icon_color: '#8a2be2' # 标题前缀图标颜色（例如：'#F47466'）
```
## 04 分享系统配置
博客根目录下`_config.butterfly.yml`文件的`分享系统配置`的代码如下：
```yaml
share: 
  # 若不需要分享功能，留空即可。 
  use: sharejs # 选择分享插件：sharejs 或 addtoany 
  # Share.js  插件配置 
  # 更多信息请参考：https://github.com/overtrue/share.js  
  sharejs: 
    sites: facebook,twitter,wechat,weibo,qq    # 可分享到的平台，多个平台用逗号分隔 
  # AddToAny 插件配置 
  # 更多信息请参考：https://www.addtoany.com/  
  addtoany: 
    item: facebook,twitter,wechat,sina_weibo,facebook_messenger,email,copy_link    # 可分享到的平台，多个平台用逗号分隔  

```

