---
title: butterfly主题魔改09：页脚美化和右下角按钮设置
categories: 博客搭建
tags:
  - hexo
  - butterfly
description: >-
  本文聚焦页脚与右下角功能按钮的深度定制。页脚部分通过注入HTML和CSS代码，实现居中布局的社交图标链接，搭配动态悬浮效果与渐变背景，并添加访问量统计脚本（支持本地存储模拟增长）。右下角按钮设置涵盖繁简转换、阅读模式、暗黑模式等功能开关，允许调整按钮顺序与显示逻辑。配置文件详细说明了按钮位置、自动切换暗黑模式的时间规则，以及滚动百分比显示等细节。最终效果使页脚兼具美观与实用性，右下角按钮提升用户操作便捷性。
top_img: /img/123.jpg
cover: /img/124.png
abbrlink: aa370e8f
date: 2025-04-08 04:52:00
updated: 2025-04-08 04:52:00
swiper_index:
---
# butterfly主题魔改09：页脚美化和右下角按钮设置
## 01 页脚自定义文本
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509161030049.png?imageSlim)
博客根目录下`_config.butterfly.yml`文件
```yaml
# --------------------------------------
# 页脚设置
# --------------------------------------
footer:
  owner:
    enable: false  # 是否显示网站所有者信息
    since: 2025   # 网站创建年份
  custom_text: |  # 自定义页脚文本（支持HTML）
    <style>
      .footer {
        text-align: center;
        position: relative;
      }
      .social-links {
        display: flex;
        justify-content: center;
        gap: 1.5rem;
        flex-wrap: wrap;
      }
      .social-links i {
        color: #8400ff;
      }
      .social-link {
        color: #8a2be2;
        font-size: 1.2rem;
        transition: all 0.3s ease;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        width: 2.5rem;
        height: 2.5rem;
        border-radius: 50%;
        background: rgba(138, 43, 226, 0.1);
      }
      .social-link:hover {
        color: #892be294;
        background: #892be294;
        transform: translateY(-3px) scale(1.2);
        box-shadow: 0 5px 15px rgba(138, 43, 226, 0.4);
        text-decoration: none !important; 
      }
      .footer p {
        margin: 0.5rem 0;
        line-height: 1;
      }
      .copyright {
        font-size: 1.1rem; 
        color: #c08bdf;
        font-weight: 400;
      }
      .tagline {
        font-size: 0.8rem;
        color: #8a2be2;
        font-style: italic;
        font-weight: 500;
      }
      .visitor-count {
        font-size: 0.75rem;
        color: rgba(219, 142, 255, 0.658);
        font-weight: 300;
      }
      #visitorCount {
        font-weight: bold;
      }
    </style>
    <div class="footer">
      <div class="social-links">
        <a href="https://github.com/kukual" class="social-link" target="_blank" rel="noopener noreferrer" aria-label="GitHub" title="GitHub">
          <i class="fab fa-github"></i>
        </a>
        <a href="https://blog.csdn.net/weixin_74811095" class="social-link" target="_blank" rel="noopener noreferrer" aria-label="CSDN" title="CSDN">
          <i class="fas fa-code"></i>
        </a>
        <a href="https://www.xiaohongshu.com/user/profile/5e8a0aae0000000001002ce4" class="social-link" target="_blank" rel="noopener noreferrer" aria-label="小红书" title="小红书">
          <i class="fas fa-book"></i>
        </a>
        <a href="https://space.bilibili.com/498478848" class="social-link" target="_blank" rel="noopener noreferrer" aria-label="bilibili" title="bilibili">
          <i class="fab fa-bilibili"></i>
        </a>
      </div>
      <p class="copyright">© 2025 kukualのblog - 所有权利保留</p>
      <p class="tagline">> Stay curious, stay hacking, stay anime! <</p>
      <p class="visitor-count">访问量: <span id="visitorCount">1024</span> | 你是第 <span id="dailyVisitor">1</span> 位今日访客</p>
    </div>
    <script>
      // 确保DOM加载完成后执行
      document.addEventListener('DOMContentLoaded', function() {
        // 模拟访问量增长
        function updateVisitorCount() {
          const countElement = document.getElementById('visitorCount');
          let count = parseInt(countElement.textContent) || 1024;
          // 从localStorage获取或初始化计数
          const storedCount = localStorage.getItem('totalVisitors');
          if (storedCount) {
            count = parseInt(storedCount);
            countElement.textContent = count;
          }
          // 每日访客计数
          const today = new Date().toDateString();
          const dailyData = JSON.parse(localStorage.getItem('dailyVisitors') || '{"date":"", "count":0}');
          if (dailyData.date !== today) {
            dailyData.date = today;
            dailyData.count = 0;
          }
          dailyData.count += 1;
          document.getElementById('dailyVisitor').textContent = dailyData.count;
          localStorage.setItem('dailyVisitors', JSON.stringify(dailyData));
          // 每30秒随机增加访问量
          setInterval(() => {
            count += Math.floor(Math.random() * 3);
            countElement.textContent = count;
            localStorage.setItem('totalVisitors', count.toString());
          }, 30000);
        }
        updateVisitorCount();
        // 添加点击动画效果
        const socialLinks = document.querySelectorAll('.social-link');
        socialLinks.forEach(link => {
          link.addEventListener('click', function() {
            this.style.transform = 'scale(0.9)';
            setTimeout(() => {
              this.style.transform = '';
            }, 300);
          });
        });
      });
    </script>
  copyright: false  # 是否显示主题和框架版权信息
```

## 02 右下角按钮设置
博客根目录下`_config.butterfly.yml`文件
```yaml
# -------------------------------------- 
# 右下角按钮 
# -------------------------------------- 
rightside_bottom: # 右下角按钮与底部的距离（默认单位：像素） 
translate: # 繁简中文转换设置 
  enable: false   # 是否启用繁简中文转换功能 
  default: 繁   # 按钮的默认文本 
  defaultEncoding: 2   # 网站的默认语言编码（1 - 繁体中文 / 2 - 简体中文） 
  translateDelay: 0   # 转换语言时的延迟时间（单位：无明确说明，推测可能是毫秒） 
  msgToTraditionalChinese: '繁'   # 当网站语言为简体中文时，按钮显示的文本 
  msgToSimplifiedChinese: '簡'   # 当网站语言为繁体中文时，按钮显示的文本 
# 阅读模式设置 
readmode: true # 是否启用阅读模式 
# 暗黑模式设置 
darkmode: 
  enable: true   # 是否启用暗黑模式 
  button: true   # 是否显示切换暗黑/明亮模式的按钮 
  # 是否自动切换暗黑/明亮模式 
  # autoChangeMode: 1  跟随系统设置，如果系统不支持暗黑模式，则在下午6点到早上6点切换到暗黑模式 
  # autoChangeMode: 2  固定在下午6点到早上6点切换到暗黑模式 
  # autoChangeMode: false  不自动切换，手动切换 
  autoChangeMode: false 
  start:   # 设置明亮模式的开始时间。取值范围在0到24之间。如果未设置，默认值为6 
  end:   # 设置明亮模式的结束时间。取值范围在0到24之间。如果未设置，默认值为18 
rightside_scroll_percent: true # 是否在返回顶部按钮中显示滚动百分比 
# 除非你知道这些设置的工作原理，否则不要修改以下设置 
# 选择要在右下角显示的功能项，选项包括：readmode（阅读模式）、translate（繁简转换）、darkmode（暗黑模式）、hideAside（隐藏侧边栏）、toc（目录）、chat（聊天）、comment（评论） 
# 不要重复使用相同的值 
rightside_item_order: 
  enable: false   # 是否启用右下角功能项排序设置 
  hide:   # 默认隐藏的功能项，默认值为：readmode,translate,darkmode,hideAside
  show: # 默认显示的功能项，默认值为：toc,chat,comment 
```
