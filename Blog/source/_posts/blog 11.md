---
title: butterfly主题魔改08：侧边栏及其卡片美化、文章等页面渐变背景
categories: 博客搭建
tags:
  - hexo
  - butterfly
description: >-
  本文重点改造侧边栏模块与全局页面背景。侧边栏新增毛玻璃效果卡片，包括作者信息、公告栏、分类/标签云等，通过CSS注入渐变背景与动画，适配暗黑模式。公告栏使用HTML自定义样式，突出关键内容。全局页面（如文章、分类、归档）添加半透明渐变背景，结合backdrop-filter实现模糊效果，增强视觉层次。导航栏同步优化为渐变悬浮样式。最终，侧边栏与页面背景形成统一的轻拟物风格，提升整体设计的质感与沉浸感。
top_img: /img/121.jpeg
cover: /img/122.jpeg
abbrlink: ab8ee243
date: 2025-04-07 04:52:00
updated: 2025-04-07 04:52:00
swiper_index:
---
# butterfly主题魔改08：侧边栏及其卡片美化、文章等页面渐变背景
参考文章： https://blog.liushen.fun/posts/28ae33b6/
## 01 侧边栏及其卡片美化
### 1、效果图
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509161013498.png?imageSlim)
### 2、主题配置文件修改
博客根目录下`_config.butterfly.yml`文件的`侧边栏设置`的代码如下：
```yaml
# --------------------------------------
# 侧边栏设置
# --------------------------------------
aside:
  enable: true  # 是否启用侧边栏
  hide: false  # 是否默认隐藏侧边栏
  button: true # 是否在右下角显示隐藏侧边栏的按钮
  mobile: false  # 在移动端是否显示
  position: left  # 侧边栏位置：left（左侧） / right（右侧）
  # 侧边栏显示内容
  display:
    archive: true  # 归档
    tag: true  # 标签
    category: true  # 分类
  # 作者信息卡片
  card_author:
    enable: true  # 是否显示作者卡片
    description:  # 作者描述（支持HTML）
    button:  # 关注按钮
      enable: true  # 是否显示
      icon: fab fa-github  # 按钮图标（Font Awesome）
      text: Follow Me  # 按钮文字
      link: https://kukual.github.io/  # 跳转链接
  # 公告卡片
  card_announcement:
    enable: true  # 是否显示公告卡片
    content: |
      <style>
      .announcement-card {
          --main-color: #ff00ff;
          --secondary-color: #00ffff;
          --highlight-color: #ff5500;
          position: relative;
          overflow: hidden;
      }
      .announcement-content {
          font-size: 1rem; 
          line-height: 1.2; 
          color: #ffffff;
          position: relative;
      }
      .keyword {
          color: var(--secondary-color);
          font-weight: 300;
          font-size: 1.1rem; 
      }
      .highlight {
          color: var(--main-color);
          font-weight: 1000;
          font-size: 1.2rem; 
      }
      .announcement-content ul {
          list-style-type: none;
          margin: 0.8rem 0; 
          padding-left: 1.5rem;   
      }
      </style>
      <div class="announcement-card">
          <div class="announcement-content">
              <p><span class="highlight">欢迎来到「酷库阿洛」网络安全研习录</span>！🎉</p>
              <p><strong>本平台专注于：</strong></p>
              <ul>
                  <li><span class="keyword">> 网络安全技术研究</span></li>
                  <li><span class="keyword">> 渗透测试实战案例</span></li>
                  <li><span class="keyword">> CTF竞赛解析</span></li>
                  <li><span class="keyword">> 漏洞复现分析</span></li>
              </ul>
              <p>🌟 <strong>加入我们，一起探索网络安全奥秘，提升攻防实战能力，共同守护数字世界的安宁！</strong></p>
          </div>
      </div>
  # 最新文章卡片
  card_recent_post:
    enable: true  # 是否显示
    # 显示数量（0表示显示全部）
    limit: 3
    # 排序依据：date（发布日期）/ updated（更新日期）
    sort: date
    sort_order: 4 # 自定义排序（可选）
  # 最新评论卡片
  card_newest_comments:
    enable: false  # 是否显示
    sort_order:  # 自定义排序（可选）
    limit: 6  # 显示数量
    # 数据缓存时间（单位：分钟，使用localStorage存储）
    storage: 10
    avatar: true  # 是否显示头像
  # 分类卡片
  card_categories:
    enable: true  # 是否显示
    # 显示数量（0表示显示全部）
    limit: 5
    # 分类是否展开：none（不控制）/ true（全部展开）/ false（全部折叠）
    expand: none
    sort_order: 3 # 自定义排序（可选）
  # 标签云卡片
  card_tags:
    enable: false  # 是否显示
    # 显示数量（0表示显示全部）
    limit: 40
    color: false  # 是否启用彩色标签
    # 排序方式：random（随机）/ name（按名称）/ length（按文章数量）
    orderby: random
    # 排序方向：1（升序）/ -1（降序）
    order: 1
    sort_order:  # 自定义排序（可选）
  # 归档卡片
  card_archives:
    enable: false  # 是否显示
    # 归档类型：monthly（按月）/ yearly（按年）
    type: monthly
    # 日期显示格式（例如：YYYY年MM月）
    format: MMMM YYYY
    # 排序方向：1（升序）/ -1（降序）
    order: -1
    # 显示数量（0表示显示全部）
    limit: 8
    sort_order:  # 自定义排序（可选）
  # 文章系列卡片
  card_post_series:
    enable: true  # 是否显示
    # 是否在标题显示系列名称
    series_title: true
    # 排序依据：title（标题）/ date（日期）
    orderBy: 'date'
    # 排序方向：1（升序）/ -1（降序）
    order: -1
  # 网站信息卡片
  card_webinfo:
    enable: true  # 是否显示
    post_count: true  # 是否显示文章总数
    last_push_date: true  # 是否显示最后更新日期
    sort_order: 5 # 自定义排序（可选）
    # 网站运行时间（从指定日期计算）
    # 格式：月/日/年 时间 或 年/月/日 时间
    # 留空则禁用此功能
    runtime_date: 2025/03/26/ 12:00 AM
```
### 3、主题样式文件修改
在博客根目录下`\themes\butterfly\source\css\custom.css`文件中添加如下代码：
```css
/* ===== 通用毛玻璃基础样式 ===== */
.card-widget {
  background: linear-gradient(-45deg, #e2c1ffee, #ffb6e6ee, #c9a9ffee, #ffb3fdee) !important;
}
/* 个人信息Follow me按钮 */
#aside-content > .card-widget.card-info > #card-info-btn {
  background-color: #7019c2f8;
  border-radius: 8px;
}
/* ===== 动画定义 ===== */
@keyframes Gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
/* ===== 暗夜模式适配 ===== */
[data-theme="dark"] .card-widget{
  background: rgba(45, 10, 61, 0.7) !important;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3) !important;
}
```

## 02 主页文章、分类等页面设置渐变背景
### 1、效果图
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509161013499.png?imageSlim)
### 2、样式代码
在博客根目录下`\themes\butterfly\source\css\custom.css`文件中添加如下代码：
```yaml
/*导航栏*/
.nav-fixed>#nav {
  background: linear-gradient(-45deg, #e0c1fa55, #fdbde755, #cfb5fc55, #fcbffa55) !important;
  backdrop-filter: blur(10px);
}
[data-theme="dark"] .nav-fixed>#nav{
  background: rgba(45, 10, 61, 0.7) !important;
  backdrop-filter: blur(10px);
}
/*文章页面*/
.layout>#post {
  background: linear-gradient(-45deg, #e0bcffdd, #ffd3f0dd, #d5bdffdd, #ffdafedd) !important;
}

[data-theme=dark] .layout>#post {
  background: rgba(45, 10, 61, 0.7) !important;
}

/*主页文章轮播页面*/
#recent-posts>.recent-post-item {
  background: linear-gradient(-45deg, #e0bcffdd, #ffd3f0dd, #d5bdffdd, #ffdafedd) !important;
}
[data-theme=dark] #recent-posts>.recent-post-item {
  background: rgba(45, 10, 61, 0.7) !important;
}

/*主页文章列表页面卡片*/
#recent-posts>.recent-post-items .recent-post-item{
  background: linear-gradient(-45deg, #e0bcffdd, #ffd3f0dd, #d5bdffdd, #ffdafedd) !important;
}
[data-theme=dark] #recent-posts>.recent-post-items .recent-post-item{
  background: rgba(45, 10, 61, 0.7) !important;
}
/*分类页面*/
.layout>#page {
  background: linear-gradient(-45deg, #e0bcffdd, #ffd3f0dd, #d5bdffdd, #ffdafedd) ;
}
[data-theme=dark] .layout>#page {
  background: rgba(45, 10, 61, 0.7) !important;
}

/*归档页面*/
.layout>#archive {
  background: linear-gradient(-45deg, #e0bcffdd, #ffd3f0dd, #d5bdffdd, #ffdafedd) !important;
}
[data-theme=dark] .layout>#archive {
  background: rgba(45, 10, 61, 0.7) !important;
}

/*分类点进去的页面*/
.layout>#category {
  background: linear-gradient(-45deg, #e0bcffdd, #ffd3f0dd, #d5bdffdd, #ffdafedd) !important;
}
[data-theme=dark] .layout>#category {
  background: rgba(45, 10, 61, 0.7) !important;
}

/*标签点进去的页面*/
.layout>#tag {
  background: linear-gradient(-45deg, #e0bcffdd, #ffd3f0dd, #d5bdffdd, #ffdafedd) !important;
}
[data-theme=dark] .layout>#tag {
  background: rgba(45, 10, 61, 0.7) !important;
}

.layout.hide-aside {
 max-width: 1600px;
}
/* 设置黑夜的时候，社交按钮为白色 */
[data-theme=dark] .social-icon i {
  color: rgba(188, 188, 188) !important; /* 设置为白色 */
}
```
