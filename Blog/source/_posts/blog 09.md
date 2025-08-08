---
title: butterfly主题魔改06：首页页面美化
categories: 博客搭建
tags:
  - hexo
  - butterfly
description: >-
  本文围绕首页视觉优化展开。调整顶部背景图高度与标题位置，增强首屏冲击力。启用副标题打字机效果，支持第三方API动态文案或自定义静态语录，提升个性化表达。首页文章布局改为瀑布流模式（封面图在上），并配置智能摘要截取逻辑，优化内容浏览效率。此外，通过hexo-butterfly-swiper插件添加置顶文章轮播功能，支持按日期或更新时间排序。最终实现兼具动态效果与信息密度的首页设计，兼顾美观性与用户体验。
top_img: /img/117.jpeg
cover: /img/118.jpeg
abbrlink: a3208a35
date: 2025-04-05 04:52:00
updated: 2025-04-05 04:52:00
swiper_index:
---
# butterfly主题魔改06：首页页面美化
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509160916872.gif?imageSlim)
## 01 首页顶部图大小
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509160916873.png?imageSlim)
修改了主页标题距离顶部距离，主页top_img高度。
博客根目录下`_config.butterfly.yml`文件。
```yaml
# --------------------------------------
# 首页设置
# --------------------------------------
# 默认top_img全屏，site_info在中间
# 使用默认, 都无需填写（建议默认）
index_site_info_top:  110px # 主页标题距离顶部距离  例如 300px/300em/300rem/10%
index_top_img_height: 300px #主页top_img高度 例如 300px/300em/300rem  不能使用百分比
```
## 02 网站副标题
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509160916875.gif?imageSlim)
启用首页副标题，启用打字机效果，以及相关配置。
博客根目录下`_config.butterfly.yml`文件。
```yaml
# 首页副标题设置
subtitle:
  enable: true       # 是否启用副标题
  effect: true       # 是否启用打字机效果
  loop: true         # 是否循环播放打字机效果
  # 自定义打字机效果配置（基于typed.js）
  # 官方配置文档：https://github.com/mattboldt/typed.js/#customization
  typed_option:
  # 第三方文案来源（目前仅支持中文）
  # 会先显示来源标识，再显示下方sub中的内容
  # 可选值：false/1/2/3
  # false - 禁用此功能
  # 1 - 使用 hitokoto.cn 的API
  # 2 - 使用 https://api.aa1.cn/doc/yiyan.html 的API
  # 3 - 使用 jinrishici.com 的API
  source: true
  # 如果关闭打字机效果，将只显示sub中的第一条内容
  sub:
    - '<i class="fas fa-quote-left"></i> 学无止境'
    - '<i class="fas fa-quote-left"></i> 千里之行，始于足下 —— 老子'
    - '<i class="fas fa-quote-left"></i> 读书破万卷，下笔如有神'
    - '<i class="fas fa-quote-left"></i> 吾日三省吾身'
    - '<i class="fas fa-quote-left"></i> 星光不问赶路人，时光不负有心人'
    - '<i class="fas fa-quote-left"></i> 人生没有白走的路，每一步都算数'
    - '<i class="fas fa-quote-left"></i> 保持热爱，奔赴山海'
    - '<i class="fas fa-quote-left"></i> 纸上得来终觉浅，绝知此事要躬行'
    - '<i class="fas fa-quote-left"></i> 成功的秘诀在于坚持'
    - '<i class="fas fa-quote-left"></i> The best way to predict the future is to invent it'
    - '<i class="fas fa-quote-left"></i> 生活是一场马拉松，你需要不断地奔跑'
    - '<i class="fas fa-quote-left"></i> 成功不是将来才有的，而是从决定去做的那一刻起，持续累积而成'
```
## 03 首页文章卡片双栏布局
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509160916876.png?imageSlim)
首页文章双栏布局设置，文章摘要显示设置。
博客根目录下`_config.butterfly.yml`文件的`首页设置`的相关修改代码如下：
```yaml
# 首页文章布局方式
# 1: 封面图在左，信息在右
# 2: 封面图在右，信息在左
# 3: 封面图与信息左右交替排列
# 4: 封面图在上，信息在下
# 5: 信息直接显示在封面图上
# 6: 瀑布流布局 - 封面图在上，信息在下
# 7: 瀑布流布局 - 信息直接显示在封面图上
index_layout: 6
```
## 04 首页文章摘要显示设置
博客根目录下`_config.butterfly.yml`文件。
```yaml
# 首页文章摘要显示设置
# 1: 显示文章描述的description
# 2: 智能显示（存在description则显示，否则显示自动截取的内容）
# 3: 自动截取内容（默认，从前N个字符截取）
# false: 不显示文章摘要
index_post_content:
  method: 1         # 选择摘要显示方式
  length: 300       # 当method为2或3时，指定截取长度（单位：字符）
```
## 05 首页文章置顶轮播插件及设置
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509160916877.gif?imageSlim)
1. 安装插件
```bash
npm install hexo-butterfly-swiper --save
```
2. 在根目录的`_config.butterfly.yml`文件后添加以下代码：
```yaml
# hexo-butterfly-swiper
# see https://akilar.top/posts/8e1264d1/
swiper:
  enable: true # 开关
  priority: 5 #过滤器优先权
  enable_page: / # 应用页面
  timemode: date #date/updated
  layout: # 挂载容器类型
    type: id
    name: recent-posts
    index: 0
  default_descr: 再怎么看我也不知道怎么描述它的啦！
  swiper_css: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiper.min.css #swiper css依赖
  swiper_js: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiper.min.js #swiper js依赖
  custom_css: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiperstyle.css # 适配主题样式补丁
  custom_js: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiper_init.js # swiper初始化方法
```
3. 在文章的头部添加属性`swiper_index`，置顶轮播图顺序，需填非负整数，数字越大越靠前
