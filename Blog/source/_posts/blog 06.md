---
title: butterfly主题魔改03：导航栏设置（标题、菜单、搜索按钮）
categories: 博客搭建
tags:
  - butterfly
  - hexo
description: 教程分三部分：1）导航栏标题与Logo配置；2）菜单居中改造（修改Pug模板与CSS样式）；3）本地搜索功能集成与界面美化。通过代码片段展示如何添加分类/标签/留言板页面，并安装hexo-generator-search插件。亮点是二次元风格的搜索框魔改，包含动态高亮关键词、滚动条特效、移动端适配，大幅提升交互体验。
top_img: /img/111.jpeg
cover: /img/112.jpeg
abbrlink: 4cb43628
date: 2025-04-02 04:52:00
updated: 2025-04-02 04:52:00
swiper_index:
---
# butterfly主题魔改03：导航栏设置（标题、菜单、搜索按钮）
## 效果图
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509150653314.png?imageSlim)
## 01 导航栏标题
### 1. 网站标题等信息设置
博客的根目录下`_config.yml`文件，修改网站信息部分如下：
```yaml
# 网站信息
title: kukualのblog  # 网站标题
subtitle: '「酷库阿洛」的网络安全研习录' # 网站副标题
description: '专注于网络安全技术研究 | 渗透测试实战案例 | CTF竞赛解析 | 漏洞复现分析'  # 网站描述，用于SEO
keywords:  # 网站关键词，用于SEO
  - 网络安全
  - 渗透测试
  - CTF竞赛
  - 漏洞分析
  - 红队技术
  - 安全开发
  - 代码审计
  - 逆向工程
  - 二进制分析
  - 漏洞复现
  - 安全工具
  - 安全策略
  - 网络防御
  - 网络安全
  - 信息安全
author: kukual  # 作者名称
language: zh-CN# 网站语言
timezone: ''  # 时区，默认使用电脑的时区
```
### 2. 博客根目录下`_config.butterfly.yml`，`nav`模块。
```yaml
nav:
  # 导航栏Logo图片路径
  logo: /img/01.png
  # 是否显示网站标题
  display_title: true
  fixed: true  # 启用滚动时固定导航栏
  bg: "#6a0dad" # 使用主题主色调
  text_color: "#ffffff" # 白色文字更清晰
  hover_color: "#e6d3ff" # 浅紫色悬停效果
```
### 3. sec增强
1. 固定链接优化：hexo-abbrlink
**作用**：将默认的层级过深的链接（如 `/2025/04/25/my-post/`）转换为固定短链接（如 `/post/cd6eb56d/`），避免中文路径问题并提升搜索引擎友好性。

```bash
npm install hexo-abbrlink --save
```

**配置**（在 根目录下`_config.yml` 中添加）：
```yaml
permalink: posts/:abbrlink/
abbrlink:
  alg: crc32  # 算法可选 crc16（默认）或 crc32
  rep: hex    # 进制可选 dec（默认）或 hex
```
2. 自动添加外链 nofollow：hexo-autonofollow
**作用**：自动为所有外部链接添加 `rel="nofollow"` 属性，防止权重流失。
```bash
npm install hexo-autonofollow --save
```
**配置**：（在 根目录下`_config.yml` 中添加）：
```yaml
nofollow:
  enable: true
  exclude:
    - yourdomain.com  # 排除自身域名或友链
```
## 02 导航栏菜单
### 1. 导航栏菜单居中设置
导航栏菜单居中，需要修改以下==两个文件==：
#### 布局模板文件
根目录下`themes\butterfly\layout\includes\header\nav.pug`
```pug
nav#nav
  // 左侧博客信息区域
  span#blog-info
    a.nav-site-title(href=url_for('/'))
      if theme.nav.logo
        img.site-icon(src=url_for(theme.nav.logo) alt='Logo')
      if theme.nav.display_title
        span.site-name=config.title
    if globalPageType === 'post'
      a.nav-page-title(href=url_for('/'))
        span.site-name=(page.title || config.title)

  // 新增的导航菜单容器（居中布局关键）
  #nav-menus-container
    // 菜单主体部分
    #menus
      // 搜索按钮
      if theme.search.use
        #search-button
          span.site-page.social-icon.search
            i.fas.fa-search.fa-fw
            span= ' ' + _p('search.title')
      
      // 菜单项
      if theme.menu
        != partial('includes/header/menu_item', {}, {cache: true})

    // 移动端汉堡菜单按钮（保持原位置）
    #toggle-menu
      span.site-page
        i.fas.fa-bars.fa-fw
```
#### 样式文件
根目录下`themes\butterfly\source\css\_layout\head.styl`，找到`#nav`导航栏基础样式部分，修改部分内容。
```stylus
// ==============================================
// butterfly主题导航栏样式表
// 功能：定义网站顶部导航栏的样式，包括菜单项、下拉菜单、搜索按钮等交互元素
// ==============================================
// 导航栏基础样式
#nav
  position: absolute
  top: 0
  z-index: 90
  display: flex
  justify-content: center  // 新增：让导航内容居中
  align-items: center
  padding: 0 36px
  width: 100%
  height: 60px
  font-size: 1.3em
  opacity: 0
  transition: all .5s
  font-family: 'Comic Sans MS', '幼圆', 'Yuanti SC', cursive, sans-serif
  letter-spacing: 0.5px // 可选：微调字间距

  +maxWidth768()
    padding: 0 16px

  &.show
    opacity: 1

  #blog-info
    position: absolute  // 修改：将博客信息定位到左侧
    left: 36px          // 左侧间距
    flex: 0             // 取消 flex 拉伸
    font-size: 1.5em
    color: var(--light-grey)
    @extend .limit-one-line

    +maxWidth768()
      left: 16px

    .site-icon
      margin-right: 6px
      height: 36px
      vertical-align: middle

    .nav-page-title
      display: none

  #toggle-menu
    display: none
    padding: 2px 0 0 6px
    vertical-align: top

    &:hover
      color: var(--white)

  a,
  span.site-page
    color: var(--light-grey)

    &:hover
      color: var(--white)

  .site-name
    text-shadow: 2px 2px 4px rgba($dark-black, .15)
    font-weight: bold

  .menus_items
    display: inline-block  // 改为 inline-block 方便居中
    margin: 0 auto         // 水平居中
    text-align: center     // 子元素居中

    .menus_item
      position: relative
      display: inline-block
      padding: 0 0 0 14px

      &:hover
        .menus_item_child
          display: block

        & > span > i:last-child
          transform: rotate(180deg)

      & > span > i:last-child
        padding: 4px
        transition: transform .3s

      .menus_item_child
        position: absolute
        right: 0
        display: none
        margin-top: 8px
        padding: 0
        width: max-content
        background-color: var(--sidebar-bg)
        box-shadow: 0 5px 20px -4px rgba($dark-black, .5)
        animation: sub_menus .3s .1s ease both
        addBorderRadius(5)

        &:before
          position: absolute
          top: -8px
          left: 0
          width: 100%
          height: 20px
          content: ''

        li
          list-style: none

          &:hover
            background: var(--text-bg-hover)

          if hexo-config('rounded_corners_ui')
            &:first-child
              border-top-left-radius: 5px
              border-top-right-radius: 5px

            &:last-child
              border-bottom-right-radius: 5px
              border-bottom-left-radius: 5px

          a
            display: inline-block
            padding: 8px 16px
            width: 100%
            color: var(--font-color) !important
            text-shadow: none !important

  &.hide-menu
    #toggle-menu
      display: inline-block !important

      .site-page
        font-size: inherit

    .menus_items
      display: none

    #search-button span:not(.site-page)
      display: none

  #search-button
    display: inline
    position: absolute
    right: 36px
    padding: 0
    color: var(--light-grey)

    +maxWidth768()
      right: 16px

    &:hover
      color: var(--white)

  .site-page
    position: relative
    padding-bottom: 6px
    text-shadow: 1px 1px 2px rgba($dark-black, .3)
    font-size: .78em
    cursor: pointer

    &:not(.child)
      &:after
        position: absolute
        bottom: 0
        left: 0
        z-index: -1
        width: 0
        height: 3px
        background-color: lighten($theme-color, 30%)
        content: ''
        transition: all .3s ease-in-out
        addBorderRadius()

      &:hover
        &:after
          width: 100%
```
### 2. 修改配置文件
菜单配置，修改根目录下`_config.butterfly.yml`文件
```yaml 
# 菜单配置（格式：菜单名: 路径 || 图标类）
# 支持二级菜单（缩进两个空格）
menu:
  首页: / || fas fa-home
  归档: /archives/ || fas fa-archive
  分类: /categories/ || fas fa-folder-open
  标签: /tags/ || fas fa-tags
  留言板: /comments/ || fas fa-comments
  关于: /about/ || fas fa-user
```
### 3. 创建对应的页面
在bash中创建菜单栏对应的页面，并修改对应的index.md文件
1. 创建分类页面
```bash
hexo new page categories
```
2. 创建标签页面
```bash
hexo new page tags
```
在根目录的`source/tags/index.md`添加`type：”tags“`
```
---
title: tags
date: 2025-04-20 14:35:39
type: ”tags“
---
```
3. 创建留言板页面
```bash
hexo new page comments
```
2. 创建关于页面
```bash
hexo new page about
```
### 4. 安装插件
标签聚合页需安装`hexo-generator-tag`，安装命令：
```bash
npm install hexo-generator-tag --save
```
分类聚合页需安装`hexo-generator-category`，安装命令：
```bash
npm install hexo-generator-category --save
```
## 03 导航栏搜索功能配置
### 1. 安装搜索插件
安装命令
```bash
npm install hexo-generator-search --save
```
### 2. 搜索按钮位置修改
 搜索按钮位置修改，需要修改以下两个文件：
#### 布局模板文件
根目录下`themes\butterfly\layout\includes\header\nav.pug`
```pug
nav#nav
  // 左侧博客信息区域
  span#blog-info
    a.nav-site-title(href=url_for('/'))
      if theme.nav.logo
        img.site-icon(src=url_for(theme.nav.logo) alt='Logo')
      if theme.nav.display_title
        span.site-name=config.title
    if globalPageType === 'post'
      a.nav-page-title(href=url_for('/'))
        span.site-name=(page.title || config.title)

  // 新增的导航菜单容器（居中布局关键）
  #nav-menus-container
    // 菜单主体部分
    #menus
      // 菜单项
      if theme.menu
        != partial('includes/header/menu_item', {}, {cache: true})

  // 右侧功能区域（新增容器）
  #nav-right-container
    // 搜索按钮（移动到右侧）
    if theme.search.use
      #search-button
        span.site-page.social-icon.search
          i.fas.fa-search.fa-fw
          span= ' ' + _p('search.title')
    
    // 移动端汉堡菜单按钮
    #toggle-menu
      span.site-page
        i.fas.fa-bars.fa-fw
```
#### 样式文件
根目录下`themes\butterfly\source\css\_layout\head.styl`，找到`#nav`导航栏基础样式部分，修改部分内容。
```stylus
// 导航栏基础样式
#nav
  // ...（保持其他样式不变）

  // 新增右侧容器样式
  #nav-right-container
    flex: none  // 禁止弹性收缩
    display: flex
    align-items: center
    gap: 15px  // 元素间距

    // 搜索按钮专属样式
    #search-button
      position: relative
      display: inline-block
      cursor: pointer
      transition: all .3s

      .search
        font-size: .85em
        padding: 4px 8px
        addBorderRadius(15px)
        transition: all .3s

        &:hover
          background: rgba(255, 255, 255, 0.73)

  // 移动端适配
  +mobile()
    #nav-menus-container
      justify-content: flex-end  // 右对齐
      #menus
        display: none  // 隐藏桌面菜单
    #nav-right-container
      #search-button
        display: none  // 移动端隐藏搜索按钮

    #toggle-menu
      display: inline-block  // 显示汉堡菜单

  // 保持其他原有样式不变...
```
### 3. 修改配置文件
修改根目录下`_config.butterfly.yml`文件
```yaml
search: 
  # 选择搜索方式：algolia_search（Algolia 搜索） / local_search（本地搜索） / docsearch（Docsearch 搜索） 
  # 若不需要搜索功能，留空即可。 
  use: local_search
  # 搜索框默认提示文字（支持多语言）
  placeholder: "输入关键词…" 
 
  # Algolia 搜索配置 
  algolia_search: 
    # 每页显示的搜索结果数量 
    hitsPerPage: 6 
 
  # 本地搜索配置 
  local_search: 
    enable: true      # 是否启用本地搜索
    # 界面文本定制
    labels:
      input_placeholder: "输入关键词…" 
      hits_empty: "没有找到与「${query}」相关的内容 😭"  # 空搜索结果提示
    # 动画效果配置
    animation: 
      enable: true    # 是否启用动画效果
      duration: 0.3   # 动画持续时间（秒）
    # 是否在页面加载时预加载搜索数据，设置为 true 预加载，false 不预加载 
    preload: ture 
    # 每篇文章显示的前 n 条搜索结果，设置为 -1 显示所有结果 
    top_n_per_article: 1 
    # 是否将 HTML 字符串转换为可读文本，设置为 true 转换，false 不转换 
    unescape: false 
    # 本地搜索所需的 CDN 地址 
    CDN: 
```
## 04 搜索功能魔改
### 1.效果图
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509150653315.png?imageSlim)
### 2.修改文件
根目录下`themes\butterfly\source\css\_search\local-search.styl`  
删除原有的，复制粘贴下面代码，保存。
```stylus
/* ================== 二次元浅紫漫画风格搜索组件样式 ==================
 * 功能描述：为Butterfly主题实现一个漫画风格的动态搜索组件，主要特点包括：
 *   - 浅紫色系渐变背景配合漫画网点纹理 
 *   - 气泡对话框设计带指示箭头 
 *   - 卡通风格的输入框与交互反馈动画 
 *   - 漫画气泡式搜索结果呈现 
 *   - 关键词高亮特效与动态图标 
 *   - 移动端响应式适配 
 * 核心特性：
 *   - 使用CSS伪元素实现对话框箭头和装饰元素 
 *   - backdrop-filter实现毛玻璃模糊效果 
 *   - 自定义滚动条样式匹配整体设计 
 *   - CSS动画实现悬停交互和视觉反馈 
 *   - SVG实现加载动画 
 * 适用场景：动漫类博客、创意类网站的搜索功能 
 * 文件位置：butterfly/source/css/_search/local-search.styl  
 * 版本：v2.1 
 * ================================================================ */
 
// 主对话框容器样式 
#local-search 
  .search-dialog 
    background: rgba(188, 170, 226, 0.98)  // 浅紫色半透明背景 
    backdrop-filter: blur(6px) saturate(180%)  // 背景模糊+饱和度提升 
    border: 3px solid #e8dfff  // 浅紫色边框 
    box-shadow: 0 8px 32px rgba(200, 180, 255, 0.2), 0 0 20px rgba(255, 255, 255, 0.6) inset  // 外阴影+内发光 
    border-radius: 16px  // 大圆角边框 
    font-family: 'Comic Neue', cursive  // 手写风格字体 
 
  // ========== 搜索输入区域 ==========
  .local-search-box 
    position: relative 
    margin-bottom: 1.2rem  // 底部间距 
 
    input 
      background: white !important  // 白色背景 
      border: 3px solid #d8c4ff !important  // 紫色边框 
      color: #6a4c9e !important  // 深紫色文字 
      width: 100%
      border-radius: 30px  // 胶囊形状 
      padding: 12px 55px 12px 35px  // 内边距（右侧留出图标空间）
      font-size: 1.05em 
      font-weight: 600  // 加粗字体 
      letter-spacing: 0.8px  // 字符间距 
      box-shadow: 0 4px 12px rgba(180,160,255,0.2), 0 2px 0 rgba(255,255,255,0.8) inset  // 外阴影+内高光 
      transition: all 0.3s cubic-bezier(0.68, -0.55, 0.27, 1.55)  // 弹性动画过渡 
 
      // 占位符样式 
      &::placeholder 
        color: #b8a5e3  // 浅紫色文字 
        font-style: italic  // 斜体 
        text-shadow: 0 1px 2px rgba(255,255,255,0.5)  // 文字投影 
 
      // 聚焦状态样式 
      &:focus 
        border-color: #ff9dff !important  // 粉色边框 
        box-shadow: 0 0 25px rgba(255,157,255,0.3), 0 6px 0 rgba(255,157,255,0.2) inset  // 发光效果 
        padding-right: 60px  // 右侧扩展 
        transform: translateY(-2px)  // 轻微上浮 
 
    // 星星装饰图标 
    &::after 
      content: '\f005'  // FontAwesome星星图标 
      font-family: 'Font Awesome 5 Free'
      font-weight: 900 
      position: absolute 
      right: 25px  // 右侧定位 
      top: 50%
      transform: translateY(-50%) rotate(15deg)  // 居中+旋转 
      color: #ff9dff  // 粉色 
      font-size: 1.4em 
      text-shadow: 0 2px 4px rgba(255,157,255,0.3)  // 图标阴影 
      transition: all 0.3s ease  // 过渡动画 
 
    // 悬停时星星效果 
    &:hover::after 
      transform: translateY(-50%) rotate(0deg) scale(1.2)  // 旋转复位+放大 
      color: #ff6bff  // 亮粉色 
 
  // ========== 搜索结果区域 ==========
  .search-result-list 
    border-radius: 12px 
    padding: 15px 
    margin: 0 -15px  // 负边距对齐 
    border: 2px solid rgb(220, 211, 243)  // 浅紫色边框 
    box-shadow: 0 4px 12px rgba(200,180,255,0.15) inset  // 内阴影 
    
    //&::-webkit-scrollbar-thumb /* 滚动条滑块样式 */
      //background: #d8c4ff
      //border-radius: 4px
      //border: 2px solid white
    // 滚动容器设置 
    .search-result-list 
      max-height: 60vh  // 最大高度 
      overflow-y: auto  // 垂直滚动 
      // 滚动条轨道 
      &::-webkit-scrollbar-track 
        background: rgba(232, 223, 255, 0.3)  // 半透明背景 
        border-radius: 10px 
        margin: 8px 0 
        border: 2px dashed rgba(200, 180, 255, 0.5)  // 虚线边框 
      
      // 滚动条滑块 
      &::-webkit-scrollbar-thumb 
        background: linear-gradient(45deg,rgb(222, 206, 255),rgb(171, 124, 247))  // 紫色渐变 
        border-radius: 10px 
        //border: 2px solid white  // 白色边框 
        box-shadow: inset 0 0 3px rgba(0,0,0,0.1)  // 内阴影 
      
      // 滚动条尺寸 
      &::-webkit-scrollbar 
        width: 10px 
        height: 10px 
 
  // ========== 单个搜索结果项 ==========
  .local-search-hit-item 
    background: white  // 白色背景 
    margin: 10px 0 
    padding: 15px 20px 
    border-radius: 10px 
    border: 2px solid #e8dfff  // 浅紫色边框 
    position: relative 
    transition: all 0.3s ease  // 过渡动画 
 
    // 左侧小三角装饰 
    &::before 
      content: ''
      position: absolute 
      left: -12px 
      top: 15px 
      width: 0 
      height: 0 
      border-style: solid 
      border-width: 8px 12px 8px 0  // 创建右侧三角形 
      border-color: transparent #e8dfff transparent transparent  // 浅紫色 
 
    // 悬停效果 
    &:hover 
      transform: translateX(8px)  // 向右移动 
      box-shadow: 6px 6px 0 rgba(200,180,255,0.3)  // 投影效果 
      background: linear-gradient(145deg, #ffffff, #faf5ff)  // 渐变背景 
 
      &::before 
        border-color: transparent #ff9dff transparent transparent  // 变为粉色 
 
    // 链接样式 
    a 
      color: #8a6dca !important  // 紫色链接 
      text-decoration: none 
      position: relative 
 
      // 链接悬停效果 
      &:hover 
        color: #ff6bff !important  // 亮粉色 
        text-decoration: underline wavy #ff9dff  // 波浪下划线 
 
    // 标题样式 
    .search-result-title 
      font-size: 1.15em 
      color: #6a4c9e !important  // 深紫色 
      text-shadow: 0 2px 2px rgba(0,0,0,0.05)  // 文字阴影 
 
    // 内容预览样式 
    .search-result 
      color: #8870a8  // 浅紫色文字 
      line-height: 1.7  // 宽松行高 
 
// ========== 关键词高亮特效 ==========
.search-keyword 
  color: #ff6bff !important  // 亮粉色 
  position: relative 
  padding: 0 2px 
  // 斜向渐变背景 
  background: linear-gradient(45deg, transparent 30%, rgba(255,107,255,0.15) 50%, transparent 70%)
  animation: sparkle 1s infinite linear  // 流光动画 
 
  // 关键词后的装饰星星 
  &::after 
    content: '☆'  // 星星符号 
    position: absolute 
    right: -12px 
    top: -8px 
    font-size: 0.8em 
    color: #ff9dff 
    animation: twinkle 1.5s infinite  // 闪烁动画 
 
// 流光动画（左右移动）
@keyframes sparkle 
  0% { background-position: -100% 0 }
  100% { background-position: 200% 0 }
 
// 星星闪烁动画 
@keyframes twinkle 
  0%, 100% { opacity: 0.3; transform: scale(0.8) }
  50% { opacity: 1; transform: scale(1.2) }
 
// ========== 新增功能样式 ==========
 
// 1. 加载动画 
.search-loading 
  display: none  // 默认隐藏 
  text-align: center 
  padding: 20px 
  
  // 激活状态 
  &.active 
    display: block 
  
  // 旋转的星星图标 
  .loading-sparkle 
    display: inline-block 
    width: 40px 
    height: 40px 
    background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg"   viewBox="0 0 24 24"><path fill="%23ff9dff" d="M12,2L4,12L12,22L20,12L12,2M12,5L16.5,12L12,19L7.5,12L12,5Z"/></svg>') no-repeat center 
    animation: spin-sparkle 1.2s linear infinite 
  
  // 加载文字 
  .loading-text 
    color: #8a6dca 
    margin-top: 10px 
    font-weight: bold 
    text-shadow: 0 1px 0 white 
 
// 星星旋转动画 
@keyframes spin-sparkle 
  0% 
    transform: rotate(0deg) scale(1)
    opacity: 1 
  50% 
    transform: rotate(180deg) scale(1.2)
    opacity: 0.7 
  100% 
    transform: rotate(360deg) scale(1)
    opacity: 1 
 
// 2. 空状态提示 
.search-empty 
  display: none  // 默认隐藏 
  text-align: center 
  padding: 30px 20px 
  
  // 激活状态 
  &.active 
    display: block 
  
  // 图标样式 
  .empty-icon 
    font-size: 3em 
    color: #d8c4ff 
    margin-bottom: 15px 
    text-shadow: 0 2px 0 white 
  
  // 标题样式 
  .empty-title 
    color: #6a4c9e 
    font-size: 1.2em 
    margin-bottom: 10px 
  
  // 描述文字 
  .empty-desc 
    color: #8870a8 
    font-style: italic 
 
// 3. 移动端适配 
@media screen and (max-width: 768px)
  #local-search 
    .search-dialog 
      width: 90vw !important  // 宽度调整为90%视口 
      left: 5vw !important  // 水平居中 
      
      // 隐藏对话框箭头 
      &::before 
        display: none 
    
    // 调整结果列表高度 
    .search-result-list 
      max-height: 50vh 
    
    // 调整结果项样式 
    .local-search-hit-item 
      padding: 12px 15px 
      
      // 调整三角箭头大小 
      &::before 
        left: -10px 
        top: 12px 
        border-width: 6px 10px 6px 0 
 
// 4. 结果数量提示 
.search-result-count 
  position: sticky  // 粘性定位 
  top: 0 
  background: rgba(245, 240, 255, 0.9)  // 半透明背景 
  backdrop-filter: blur(5px)  // 背景模糊 
  padding: 8px 15px 
  margin: -15px -15px 15px  // 负边距对齐 
  border-bottom: 2px solid #e8dfff  // 底部边框 
  z-index: 1  // 层级控制 
  color: #8a6dca 
  font-weight: bold 
  
  // 关键词样式 
  .search-keyword 
    color: #ff6bff 
    padding: 0 4px 
```
