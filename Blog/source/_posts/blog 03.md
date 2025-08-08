---
title: hexo butterfly主题整体结构解析
categories: 博客搭建
tags:
  - hexo
  - butterfly
description: 全面解析Butterfly主题的模块化目录结构，从根目录的配置文件（_config.yml、plugins.yml）到核心功能模块（布局文件、样式脚本、静态资源）逐一说明。重点标注了layout/下的Pug模板组件（如头部、侧边栏、评论系统）、source/中的CSS/JS定制入口，以及scripts/的事件处理逻辑。适合开发者深度定制主题时快速定位文件，理解各模块的依赖关系与修改影响。
top_img: /img/105.jpeg
cover: /img/106.jpeg
abbrlink: 8ac25d19
date: 2025-03-30 04:52:00
updated: 2025-03-30 04:52:00
swiper_index: 3
---
# Hexo Butterfly主题目录结构
## Butterfly主题采用模块化设计，以下是主题的目录结构
```js
themes/butterfly/
├── _config.yml
├── .gitignore
├── _config.butterfly.yml
├── package.json
├── plugins.yml
├── .github/
│   ├── ISSUE _TEMPLATE/
│   │   ├── bug_report.yml
│   │   ├── config.yml 
│   │   ├── feature_request.yml
│   ├── workflows/
│   │   ├── publish.yml
│   │   ├── stale.yml
│   ├── FUNDING.yml
├── languages/
├── layout/
│   ├── includes/
│   │   ├── head/
│   │   │   ├──analytics.pug
│   │   │   ├──config_site.pug
│   │   │   ├──config.pug
│   │   │   ├──google _adsense.pug
│   │   │   ├──Open_Graph.pug
│   │   │   ├──preconnect.pug
│   │   │   ├──pwa.pug
│   │   │   ├──site_verification.pug
│   │   │   ├──structured_data.pug
│   │   ├── header/
│   │   │   ├──index.pug
│   │   │   ├──menu_item.pug
│   │   │   ├──nav.pug
│   │   │   ├──post-info.pug
│   │   │   ├──social.pug
│   │   ├── loading/
│   │   │   ├──fullpage-loading.pug
│   │   │   ├──index.pug
│   │   │   ├──pace.pug
│   │   ├── mixins/
│   │   │   ├──article-sort.pug
│   │   │   ├──indexPostUl.pug
│   │   ├── page/
│   │   │   ├──404.pug
│   │   │   ├──categories.pug
│   │   │   ├──default-page.pug
│   │   │   ├──flink.pug
│   │   │   ├──shuoshuo.pug
│   │   │   ├──tags.pug
│   │   ├── post/
│   │   │   ├──outdate-notice.pug
│   │   │   ├──post-copyright.pug
│   │   │   ├──reward.pug
│   │   ├── third-party/
│   │   │   ├──abcjs/
│   │   │   │   ├──abcjs.pug
│   │   │   │   ├──index.pug
│   │   │   ├──card-post-count/
│   │   │   │   ├──artalk.pug
│   │   │   │   ├──disqus.pug
│   │   │   │   ├──fb.pug
│   │   │   │   ├──index.pug
│   │   │   │   ├──remark42.pug
│   │   │   │   ├──twikoo.pug
│   │   │   │   ├──valine.pug
│   │   │   │   ├──waline.pug
│   │   │   ├──chat/
│   │   │   │   ├──chatra.pug
│   │   │   │   ├──crisp.pug
│   │   │   │   ├──index.pug
│   │   │   │   ├──tidio.pug
│   │   │   ├──comments/
│   │   │   │   ├──artalk.pug
│   │   │   │   ├──disqus.pug
│   │   │   │   ├──disqusjs.pug
│   │   │   │   ├──facebook_comments.pug
│   │   │   │   ├──giscus.pug
│   │   │   │   ├──gitalk.pug
│   │   │   │   ├──index.pug
│   │   │   │   ├──js.pug
│   │   │   │   ├──livere.pug
│   │   │   │   ├──remark42.pug
│   │   │   │   ├──twikoo.pug
│   │   │   │   ├──utterances.pug
│   │   │   │   ├──valine.pug
│   │   │   │   ├──waline.pug
│   │   │   ├──math/
│   │   │   │   ├──chartjs.pug
│   │   │   │   ├──index.pug
│   │   │   │   ├──katex.pug
│   │   │   │   ├──mathjax.pug
│   │   │   │   ├──mermaid.pug
│   │   │   ├──newest-comments/
│   │   │   │   ├──artalk.pug
│   │   │   │   ├──common.pug
│   │   │   │   ├──disqus-comment.pug
│   │   │   │   ├──github-issues.pug
│   │   │   │   ├──index.pug
│   │   │   │   ├──remark42.pug
│   │   │   │   ├──twikoo-comment.pug
│   │   │   │   ├──valine.pug
│   │   │   │   ├──waline.pug
│   │   │   ├──search/
│   │   │   │   ├──algolia.pug
│   │   │   │   ├──docsearch.pug
│   │   │   │   ├──index.pug
│   │   │   │   ├──local-search.pug
│   │   │   ├──share/
│   │   │   │   ├──addtoany.pug
│   │   │   │   ├──index.pug
│   │   │   │   ├──share-js.pug
│   │   │   ├──aplayer.pug
│   │   │   ├──effect.pug
│   │   │   ├──pjax.pug
│   │   │   ├──prismjs.pug
│   │   │   ├──subtitle.pug
│   │   │   ├──umami_analytics.pug
│   │   ├── widget/
│   │   │   ├──card_ad.pug
│   │   │   ├──card_announcement.pug
│   │   │   ├──card_archives.pug
│   │   │   ├──card_author.pug
│   │   │   ├──card_bottom_sef.pug
│   │   │   ├──card_categories.pug
│   │   │   ├──card_newest_comment.pug
│   │   │   ├──card_post_series.pug
│   │   │   ├──card_post_toc.pug
│   │   │   ├──card_recent_post.pug
│   │   │   ├──card_tags.pug
│   │   │   ├──card_top_selfpug
│   │   │   ├──card_webinfo.pug
│   │   │   ├──index.pug
│   │   ├──additional-js.pug
│   │   ├──footer.pug
│   │   ├──head.pug
│   │   ├──layout.pug
│   │   ├──pagination.pug
│   │   ├──rightside.pug
│   │   ├──sidebar.pug
│   ├── archive.pug
│   ├── category.pug
│   ├── index.pug
│   ├── page.pug
│   ├── post.pug
│   ├── tag.pug
├── scripts/
│   ├── common/
│   │   ├──postDesc.js
│   ├── events/
│   │   ├──404.js
│   │   ├──cdn.js
│   │   ├──comment.js
│   │   ├──init.js
│   │   ├──merge_config.js
│   │   ├──stylus.js
│   │   ├──welcome.js
│   ├── filters/
│   │   ├──post_lazyload.js
│   │   ├──random_cover.js
│   ├── helpers/
│   │   ├──aside_archives.js
│   │   ├──aside_categories.js
│   │   ├──getArchivelength.js
│   │   ├──inject _head_js.js
│   │   ├──page.js
│   │   ├──related_post.js
│   │   ├──series.js
│   ├── tag/
│   │   ├──button.js
│   │   ├──chartjsjs
│   │   ├──flink.js
│   │   ├──gallery.js
│   │   ├──hide.js
│   │   ├──inlinelmg.js
│   │   ├──label.js
│   │   ├──mermaid.js
│   │   ├──note.js
│   │   ├──score.js
│   │   ├──series.js
│   │   ├──tabs.js
│   │   ├──timeline.js
├── source/
│   ├── css/
│   │   ├──_global/
│   │   │   ├──function.styl
│   │   │   ├──index.styl
│   │   ├──_highlight/
│   │   │   ├──highlight/
│   │   │   │   ├──diff.styl
│   │   │   │   ├──index.styl
│   │   │   ├──prismjs/
│   │   │   │   ├──diff.styl
│   │   │   │   ├──index.styl
│   │   │   │   ├──line-number.styl
│   │   │   ├──highlight.styl
│   │   │   ├──theme.styl
│   │   ├──_layout/
│   │   │   ├──aside.styl
│   │   │   ├──chat.styl
│   │   │   ├──comments.styl
│   │   │   ├──footer.styl
│   │   │   ├──head.styl
│   │   │   ├──loading.styl
│   │   │   ├──pagination.styl
│   │   │   ├──post.styl
│   │   │   ├──relatedposts.styl
│   │   │   ├──reward.styl
│   │   │   ├──rightside.styl
│   │   │   ├──sidebar.styl
│   │   │   ├──third-party.styl
│   │   ├──_mode/
│   │   │   ├──darkmode.styl
│   │   │   ├──readmode.styl
│   │   ├──-page/
│   │   │   ├──404.styl
│   │   │   ├──archives.styl
│   │   │   ├──categories.styl
│   │   │   ├──common.styl
│   │   │   ├──flink.styl
│   │   │   ├──homepage.styl
│   │   │   ├──shuoshuo.styl
│   │   │   ├──tags.styl
│   │   ├──_search/
│   │   │   ├──algolia.styl
│   │   │   ├──index.styl
│   │   │   ├──local-search.styl
│   │   ├──_tags/
│   │   │   ├──button.styl
│   │   │   ├──gallery.styl
│   │   │   ├──hexo.styl
│   │   │   ├──hide.styl
│   │   │   ├──inlinelmg.styl
│   │   │   ├──label.styl
│   │   │   ├──note.styl
│   │   │   ├──series.styl
│   │   │   ├──tabs.styl
│   │   │   ├──timeline.styl
│   │   ├──_third-party/
│   │   │   ├──normalize.min.css
│   │   ├──index.styl
│   │   ├──var.styl
│   ├── js/
│   │   ├──search
│   │   │   ├──algolia.js
│   │   │   ├──local-search.js
│   │   ├──main.js
│   │   ├──sakura.js
│   │   ├──tw_cn.js
│   │   ├──utils.js
│   └── img/
```
## Hexo Butterfly主题整体结构解析
```JavaScript
Hexo Butterfly主题整体结构解析
themes/butterfly/
├── _config.yml
│   // 主题的全局配置文件，用于设置主题的基本选项。
│   // 可以修改，修改后会影响主题的全局行为，比如站点标题、菜单、SEO 等。
├── .gitignore
│   // Git 忽略文件配置，用于指定哪些文件或文件夹不被 Git 版本控制。
│   // 一般不需要修改，除非需要添加或移除忽略的文件。
├── _config.butterfly.yml
│   // Butterfly 主题的专属配置文件，用于设置主题的高级选项。
│   // 可以修改，修改后会影响主题的特定功能，比如评论系统、搜索、广告等。
├── package.json
│   // 项目依赖和元数据文件，用于管理主题的 Node.js 依赖。
│   // 一般不需要修改，除非需要添加或更新依赖。
├── plugins.yml
│   // 插件配置文件，用于管理主题的插件。
│   // 可以修改，修改后会影响插件的加载和功能。
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.yml
│   │   // GitHub 仓库的 Bug 报告模板。
│   │   // 一般不需要修改，除非需要自定义 Bug 报告格式。
│   │   ├── config.yml 
│   │   // GitHub 仓库的配置文件。
│   │   // 一般不需要修改。
│   │   ├── feature_request.yml
│   │   // GitHub 仓库的功能请求模板。
│   │   // 一般不需要修改。
│   ├── workflows/
│   │   ├── publish.yml
│   │   // GitHub Actions 的发布工作流。
│   │   // 一般不需要修改。
│   │   ├── stale.yml
│   │   // GitHub Actions 的过期工作流。
│   │   // 一般不需要修改。
│   ├── FUNDING.yml
│   // GitHub 仓库的资助配置文件。
│   // 一般不需要修改。
├── languages/
│   // 语言文件夹，用于存储多语言支持的文件。
│   // 可以修改，修改后会影响主题的多语言显示。
├── layout/
│   // 布局文件夹，用于存储主题的模板文件。
│   ├── includes/
│   │   // 包含文件夹，用于存储可复用的模板组件。
│   │   ├── head/
│   │   │   // 头部相关模板。
│   │   │   ├── analytics.pug
│   │   │   // 分析工具模板。
│   │   │   // 可以修改，修改后会影响分析工具的加载。
│   │   │   ├── config_site.pug
│   │   │   // 站点配置模板。
│   │   │   // 可以修改，修改后会影响站点配置的显示。
│   │   │   ├── config.pug
│   │   │   // 配置模板。
│   │   │   // 可以修改，修改后会影响配置的显示。
│   │   │   ├── google_adsense.pug
│   │   │   // Google AdSense 模板。
│   │   │   // 可以修改，修改后会影响 AdSense 广告的显示。
│   │   │   ├── Open_Graph.pug
│   │   │   // Open Graph 模板，用于社交媒体分享。
│   │   │   // 可以修改，修改后会影响分享卡片的显示。
│   │   │   ├── preconnect.pug
│   │   │   // 预连接模板。
│   │   │   // 可以修改，修改后会影响资源预加载。
│   │   │   ├── pwa.pug
│   │   │   // PWA 模板。
│   │   │   // 可以修改，修改后会影响 PWA 功能。
│   │   │   ├── site_verification.pug
│   │   │   // 站点验证模板。
│   │   │   // 可以修改，修改后会影响站点验证。
│   │   │   ├── structured_data.pug
│   │   │   // 结构化数据模板。
│   │   │   // 可以修改，修改后会影响 SEO 结构化数据。
│   │   ├── header/
│   │   │   // 头部相关模板。
│   │   │   ├── index.pug
│   │   │   // 头部主模板。
│   │   │   // 可以修改，修改后会影响头部的显示。
│   │   │   ├── menu_item.pug
│   │   │   // 菜单项模板。
│   │   │   // 可以修改，修改后会影响菜单项的显示。
│   │   │   ├── nav.pug
│   │   │   // 导航栏模板。
│   │   │   // 可以修改，修改后会影响导航栏的显示。
│   │   │   ├── post-info.pug
│   │   │   // 文章信息模板。
│   │   │   // 可以修改，修改后会影响文章信息的显示。
│   │   │   ├── social.pug
│   │   │   // 社交链接模板。
│   │   │   // 可以修改，修改后会影响社交链接的显示。
│   │   ├── loading/
│   │   │   // 加载相关模板。
│   │   │   ├── fullpage-loading.pug
│   │   │   // 全页面加载模板。
│   │   │   // 可以修改，修改后会影响全页面加载效果。
│   │   │   ├── index.pug
│   │   │   // 加载主模板。
│   │   │   // 可以修改，修改后会影响加载效果。
│   │   │   ├── pace.pug
│   │   │   // Pace 加载动画模板。
│   │   │   // 可以修改，修改后会影响加载动画效果。
│   │   ├── mixins/
│   │   │   // 混合模板，用于复用代码。
│   │   │   ├── article-sort.pug
│   │   │   // 文章排序模板。
│   │   │   // 可以修改，修改后会影响文章排序。
│   │   │   ├── indexPostUl.pug
│   │   │   // 文章列表模板。
│   │   │   // 可以修改，修改后会影响文章列表的显示。
│   │   ├── page/
│   │   │   // 页面相关模板。
│   │   │   ├── 404.pug
│   │   │   // 404 页面模板。
│   │   │   // 可以修改，修改后会影响 404 页面的显示。
│   │   │   ├── categories.pug
│   │   │   // 分类页面模板。
│   │   │   // 可以修改，修改后会影响分类页面的显示。
│   │   │   ├── default-page.pug
│   │   │   // 默认页面模板。
│   │   │   // 可以修改，修改后会影响默认页面的显示。
│   │   │   ├── flink.pug
│   │   │   // 友链页面模板。
│   │   │   // 可以修改，修改后会影响友链页面的显示。
│   │   │   ├── shuoshuo.pug
│   │   │   // 说说页面模板。
│   │   │   // 可以修改，修改后会影响说说页面的显示。
│   │   │   ├── tags.pug
│   │   │   // 标签页面模板。
│   │   │   // 可以修改，修改后会影响标签页面的显示。
│   │   ├── post/
│   │   │   // 文章相关模板。
│   │   │   ├── outdate-notice.pug
│   │   │   // 过期文章通知模板。
│   │   │   // 可以修改，修改后会影响过期文章的显示。
│   │   │   ├── post-copyright.pug
│   │   │   // 文章版权模板。
│   │   │   // 可以修改，修改后会影响文章版权的显示。
│   │   │   ├── reward.pug
│   │   │   // 打赏模板。
│   │   │   // 可以修改，修改后会影响打赏功能的显示。
│   │   ├── third-party/
│   │   │   // 第三方服务模板。
│   │   │   ├── abcjs/
│   │   │   │   ├── abcjs.pug
│   │   │   │   // ABCJS 模板。
│   │   │   │   // 可以修改，修改后会影响 ABCJS 的显示。
│   │   │   │   ├── index.pug
│   │   │   │   // ABCJS 主模板。
│   │   │   │   // 可以修改，修改后会影响 ABCJS 的显示。
│   │   │   ├── card-post-count/
│   │   │   │   ├── artalk.pug
│   │   │   │   // Artalk 评论计数模板。
│   │   │   │   // 可以修改，修改后会影响 Artalk 评论计数的显示。
│   │   │   │   ├── disqus.pug
│   │   │   │   // Disqus 评论计数模板。
│   │   │   │   // 可以修改，修改后会影响 Disqus 评论计数的显示。
│   │   │   │   ├── fb.pug
│   │   │   │   // Facebook 评论计数模板。
│   │   │   │   // 可以修改，修改后会影响 Facebook 评论计数的显示。
│   │   │   │   ├── index.pug
│   │   │   │   // 评论计数主模板。
│   │   │   │   // 可以修改，修改后会影响评论计数的显示。
│   │   │   │   ├── remark42.pug
│   │   │   │   // Remark42 评论计数模板。
│   │   │   │   // 可以修改，修改后会影响 Remark42 评论计数的显示。
│   │   │   │   ├── twikoo.pug
│   │   │   │   // Twikoo 评论计数模板。
│   │   │   │   // 可以修改，修改后会影响 Twikoo 评论计数的显示。
│   │   │   │   ├── valine.pug
│   │   │   │   // Valine 评论计数模板。
│   │   │   │   // 可以修改，修改后会影响 Valine 评论计数的显示。
│   │   │   │   ├── waline.pug
│   │   │   │   // Waline 评论计数模板。
│   │   │   │   // 可以修改，修改后会影响 Waline 评论计数的显示。
│   │   │   ├── chat/
│   │   │   │   ├── chatra.pug
│   │   │   │   // Chatra 聊天模板。
│   │   │   │   // 可以修改，修改后会影响 Chatra 聊天功能的显示。
│   │   │   │   ├── crisp.pug
│   │   │   │   // Crisp 聊天模板。
│   │   │   │   // 可以修改，修改后会影响 Crisp 聊天功能的显示。
│   │   │   │   ├── index.pug
│   │   │   │   // 聊天主模板。
│   │   │   │   // 可以修改，修改后会影响聊天功能的显示。
│   │   │   │   ├── tidio.pug
│   │   │   │   // Tidio 聊天模板。
│   │   │   │   // 可以修改，修改后会影响 Tidio 聊天功能的显示。
│   │   │   ├── comments/
│   │   │   │   ├── artalk.pug
│   │   │   │   // Artalk 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Artalk 评论的显示。
│   │   │   │   ├── disqus.pug
│   │   │   │   // Disqus 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Disqus 评论的显示。
│   │   │   │   ├── disqusjs.pug
│   │   │   │   // Disqus.js 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Disqus.js 评论的显示。
│   │   │   │   ├── facebook_comments.pug
│   │   │   │   // Facebook 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Facebook 评论的显示。
│   │   │   │   ├── giscus.pug
│   │   │   │   // Giscus 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Giscus 评论的显示。
│   │   │   │   ├── gitalk.pug
│   │   │   │   // Gitalk 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Gitalk 评论的显示。
│   │   │   │   ├── index.pug
│   │   │   │   // 评论主模板。
│   │   │   │   // 可以修改，修改后会影响评论功能的显示。
│   │   │   │   ├── js.pug
│   │   │   │   // 评论 JS 模板。
│   │   │   │   // 可以修改，修改后会影响评论功能的 JS 加载。
│   │   │   │   ├── livere.pug
│   │   │   │   // Livere 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Livere 评论的显示。
│   │   │   │   ├── remark42.pug
│   │   │   │   // Remark42 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Remark42 评论的显示。
│   │   │   │   ├── twikoo.pug
│   │   │   │   // Twikoo 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Twikoo 评论的显示。
│   │   │   │   ├── utterances.pug
│   │   │   │   // Utterances 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Utterances 评论的显示。
│   │   │   │   ├── valine.pug
│   │   │   │   // Valine 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Valine 评论的显示。
│   │   │   │   ├── waline.pug
│   │   │   │   // Waline 评论模板。
│   │   │   │   // 可以修改，修改后会影响 Waline 评论的显示。
│   │   │   ├── math/
│   │   │   │   ├── chartjs.pug
│   │   │   │   // Chart.js 模板。
│   │   │   │   // 可以修改，修改后会影响 Chart.js 的显示。
│   │   │   │   ├── index.pug
│   │   │   │   // 数学公式主模板。
│   │   │   │   // 可以修改，修改后会影响数学公式的显示。
│   │   │   │   ├── katex.pug
│   │   │   │   // KaTeX 模板。
│   │   │   │   // 可以修改，修改后会影响 KaTeX 的显示。
│   │   │   │   ├── mathjax.pug
│   │   │   │   // MathJax 模板。
│   │   │   │   // 可以修改，修改后会影响 MathJax 的显示。
│   │   │   │   ├── mermaid.pug
│   │   │   │   // Mermaid 模板。
│   │   │   │   // 可以修改，修改后会影响 Mermaid 的显示。
│   │   │   ├── newest-comments/
│   │   │   │   ├── artalk.pug
│   │   │   │   // Artalk 最新评论模板。
│   │   │   │   // 可以修改，修改后会影响 Artalk 最新评论的显示。
│   │   │   │   ├── common.pug
│   │   │   │   // 最新评论公共模板。
│   │   │   │   // 可以修改，修改后会影响最新评论的显示。
│   │   │   │   ├── disqus-comment.pug
│   │   │   │   // Disqus 最新评论模板。
│   │   │   │   // 可以修改，修改后会影响 Disqus 最新评论的显示。
│   │   │   │   ├── github-issues.pug
│   │   │   │   // GitHub Issues 最新评论模板。
│   │   │   │   // 可以修改，修改后会影响 GitHub Issues 最新评论的显示。
│   │   │   │   ├── index.pug
│   │   │   │   // 最新评论主模板。
│   │   │   │   // 可以修改，修改后会影响最新评论的显示。
│   │   │   │   ├── remark42.pug
│   │   │   │   // Remark42 最新评论模板。
│   │   │   │   // 可以修改，修改后会影响 Remark42 最新评论的显示。
│   │   │   │   ├── twikoo-comment.pug
│   │   │   │   // Twikoo 最新评论模板。
│   │   │   │   // 可以修改，修改后会影响 Twikoo 最新评论的显示。
│   │   │   │   ├── valine.pug
│   │   │   │   // Valine 最新评论模板。
│   │   │   │   // 可以修改，修改后会影响 Valine 最新评论的显示。
│   │   │   │   ├── waline.pug
│   │   │   │   // Waline 最新评论模板。
│   │   │   │   // 可以修改，修改后会影响 Waline 最新评论的显示。
│   │   │   ├── search/
│   │   │   │   ├── algolia.pug
│   │   │   │   // Algolia 搜索功能模板。
│   │   │   │   // 可以修改，修改后会影响 Algolia 搜索功能的显示。
│   │   │   │   ├── docsearch.pug
│   │   │   │   // DocSearch 搜索结果模板。
│   │   │   │   // 可以修改，修改后会影响 DocSearch 搜索结果的显示。
│   │   │   │   ├── index.pug
│   │   │   │   // 搜索功能主模板。
│   │   │   │   // 可以修改，修改后会影响搜索功能的显示。
│   │   │   │   ├── local-search.pug
│   │   │   │   // 本地搜索模板。
│   │   │   │   // 可以修改，修改后会影响本地搜索的显示。
│   │   │   ├── share/
│   │   │   │   ├── addtoany.pug
│   │   │   │   // AddToAny 分享模板。
│   │   │   │   // 可以修改，修改后会影响 AddToAny 分享的显示。
│   │   │   │   ├── index.pug
│   │   │   │   // 分享主模板。
│   │   │   │   // 可以修改，修改后会影响分享功能的显示。
│   │   │   │   ├── share-js.pug
│   │   │   │   // 分享 JS 模板。
│   │   │   │   // 可以修改，修改后会影响分享功能的 JS 加载。
│   │   │   ├── aplayer.pug
│   │   │   // APlayer 音乐播放器模板。
│   │   │   // 可以修改，修改后会影响 APlayer 的显示。
│   │   │   ├── effect.pug
│   │   │   // 特效模板。
│   │   │   // 可以修改，修改后会影响特效的显示。
│   │   │   ├── pjax.pug
│   │   │   // PJAX 模板。
│   │   │   // 可以修改，修改后会影响 PJAX 功能的显示。
│   │   │   ├── prismjs.pug
│   │   │   // Prism.js 代码高亮模板。
│   │   │   // 可以修改，修改后会影响 Prism.js 的显示。
│   │   │   ├── subtitle.pug
│   │   │   // 副标题模板。
│   │   │   // 可以修改，修改后会影响副标题的显示。
│   │   │   ├── umami_analytics.pug
│   │   │   // Umami 分析模板。
│   │   │   // 可以修改，修改后会影响 Umami 分析的显示。
│   │   ├── widget/
│   │   │   // 小部件模板。
│   │   │   ├── card_ad.pug
│   │   │   // 广告卡片模板。
│   │   │   // 可以修改，修改后会影响广告卡片的显示。
│   │   │   ├── card_announcement.pug
│   │   │   // 公告卡片模板。
│   │   │   // 可以修改，修改后会影响公告卡片的显示。
│   │   │   ├── card_archives.pug
│   │   │   // 归档卡片模板。
│   │   │   // 可以修改，修改后会影响归档卡片的显示。
│   │   │   ├── card_author.pug
│   │   │   // 作者卡片模板。
│   │   │   // 可以修改，修改后会影响作者卡片的显示。
│   │   │   ├── card_bottom_self.pug
│   │   │   // 底部自定义卡片模板。
│   │   │   // 可以修改，修改后会影响底部自定义卡片的显示。
│   │   │   ├── card_categories.pug
│   │   │   // 分类卡片模板。
│   │   │   // 可以修改，修改后会影响分类卡片的显示。
│   │   │   ├── card_newest_comment.pug
│   │   │   // 最新评论卡片模板。
│   │   │   // 可以修改，修改后会影响最新评论卡片的显示。
│   │   │   ├── card_post_series.pug
│   │   │   // 文章系列卡片模板。
│   │   │   // 可以修改，修改后会影响文章系列卡片的显示。
│   │   │   ├── card_post_toc.pug
│   │   │   // 文章目录卡片模板。
│   │   │   // 可以修改，修改后会影响文章目录卡片的显示。
│   │   │   ├── card_recent_post.pug
│   │   │   // 最近文章卡片模板。
│   │   │   // 可以修改，修改后会影响最近文章卡片的显示。
│   │   │   ├── card_tags.pug
│   │   │   // 标签卡片模板。
│   │   │   // 可以修改，修改后会影响标签卡片的显示。
│   │   │   ├── card_top_self.pug
│   │   │   // 顶部自定义卡片模板。
│   │   │   // 可以修改，修改后会影响顶部自定义卡片的显示。
│   │   │   ├── card_webinfo.pug
│   │   │   // 网站信息卡片模板。
│   │   │   // 可以修改，修改后会影响网站信息卡片的显示。
│   │   │   ├── index.pug
│   │   │   // 小部件主模板。
│   │   │   // 可以修改，修改后会影响小部件的显示。
│   │   ├── additional-js.pug
│   │   // 额外 JS 模板。
│   │   // 可以修改，修改后会影响额外 JS 的加载。
│   │   ├── footer.pug
│   │   // 页脚模板。
│   │   // 可以修改，修改后会影响页脚的显示。
│   │   ├── head.pug
│   │   // 头部主模板。
│   │   // 可以修改，修改后会影响头部的显示。
│   │   ├── layout.pug
│   │   // 布局主模板。
│   │   // 可以修改，修改后会影响整体布局。
│   │   ├── pagination.pug
│   │   // 分页模板。
│   │   // 可以修改，修改后会影响分页的显示。
│   │   ├── rightside.pug
│   │   // 右侧边栏模板。
│   │   // 可以修改，修改后会影响右侧边栏的显示。
│   │   ├── sidebar.pug
│   │   // 侧边栏模板。
│   │   // 可以修改，修改后会影响侧边栏的显示。
│   ├── archive.pug
│   // 归档页面模板。
│   // 可以修改，修改后会影响归档页面的显示。
│   ├── category.pug
│   // 分类页面模板。
│   // 可以修改，修改后会影响分类页面的显示。
│   ├── index.pug
│   // 首页模板。
│   // 可以修改，修改后会影响首页的显示。
│   ├── page.pug
│   // 页面模板。
│   // 可以修改，修改后会影响页面的显示。
│   ├── post.pug
│   // 文章页面模板。
│   // 可以修改，修改后会影响文章页面的显示。
│   ├── tag.pug
│   // 标签页面模板。
│   // 可以修改，修改后会影响标签页面的显示。
├── scripts/
│   // 脚本文件夹，用于存储主题的 JavaScript 文件。
│   ├── common/
│   │   ├── postDesc.js
│   │   // 文章描述脚本。
│   │   // 可以修改，修改后会影响文章描述的显示。
│   ├── events/
│   │   ├── 404.js
│   │   // 404 页面事件脚本。
│   │   // 可以修改，修改后会影响 404 页面的交互。
│   │   ├── cdn.js
│   │   // CDN 脚本。
│   │   // 可以修改，修改后会影响 CDN 的加载。
│   │   ├── comment.js
│   │   // 评论事件脚本。
│   │   // 可以修改，修改后会影响评论功能的交互。
│   │   ├── init.js
│   │   // 初始化脚本。
│   │   // 可以修改，修改后会影响主题的初始化过程。
│   │   ├── merge_config.js
│   │   // 配置合并脚本。
│   │   // 可以修改，修改后会影响配置的合并逻辑。
│   │   ├── stylus.js
│   │   // Stylus 脚本。
│   │   // 可以修改，修改后会影响 Stylus 的加载。
│   │   ├── welcome.js
│   │   // 欢迎脚本。
│   │   // 可以修改，修改后会影响欢迎功能的交互。
│   ├── filters/
│   │   ├── post_lazyload.js
│   │   // 文章懒加载脚本。
│   │   // 可以修改，修改后会影响文章懒加载的功能。
│   │   ├── random_cover.js
│   │   // 随机封面脚本。
│   │   // 可以修改，修改后会影响随机封面的显示。
│   ├── helpers/
│   │   ├── aside_archives.js
│   │   // 侧边栏归档助手脚本。
│   │   // 可以修改，修改后会影响侧边栏归档的显示。
│   │   ├── aside_categories.js
│   │   // 侧边栏分类助手脚本。
│   │   // 可以修改，修改后会影响侧边栏分类的显示。
│   │   ├── getArchivelength.js
│   │   // 获取归档长度脚本。
│   │   // 可以修改，修改后会影响归档长度的计算。
│   │   ├── inject_head_js.js
│   │   // 注入头部 JS 脚本。
│   │   // 可以修改，修改后会影响头部 JS 的加载。
│   │   ├── page.js
│   │   // 页面助手脚本。
│   │   // 可以修改，修改后会影响页面功能的交互。
│   │   ├── related_post.js
│   │   // 相关文章助手脚本。
│   │   // 可以修改，修改后会影响相关文章的显示。
│   │   ├── series.js
│   │   // 系列助手脚本。
│   │   // 可以修改，修改后会影响系列文章的显示。
│   ├── tag/
│   │   ├── button.js
│   │   // 按钮脚本。
│   │   // 可以修改，修改后会影响按钮的交互。
│   │   ├── chartjsjs
│   │   // Chart.js 脚本。
│   │   // 可以修改，修改后会影响 Chart.js 的功能。
│   │   ├── flink.js
│   │   // 友链脚本。
│   │   // 可以修改，修改后会影响友链的显示。
│   │   ├── gallery.js
│   │   // 图库脚本。
│   │   // 可以修改，修改后会影响图库的显示。
│   │   ├── hide.js
│   │   // 隐藏脚本。
│   │   // 可以修改，修改后会影响隐藏功能的交互。
│   │   ├── inlinelmg.js
│   │   // 内联图片脚本。
│   │   // 可以修改，修改后会影响内联图片的显示。
│   │   ├── label.js
│   │   // 标签脚本。
│   │   // 可以修改，修改后会影响标签的显示。
│   │   ├── mermaid.js
│   │   // Mermaid 脚本。
│   │   // 可以修改，修改后会影响 Mermaid 的功能。
│   │   ├── note.js
│   │   // 笔记脚本。
│   │   // 可以修改，修改后会影响笔记的显示。
│   │   ├── score.js
│   │   // 评分脚本。
│   │   // 可以修改，修改后会影响评分功能的显示。
│   │   ├── series.js
│   │   // 系列脚本。
│   │   // 可以修改，修改后会影响系列文章的显示。
│   │   ├── tabs.js
│   │   // 标签页脚本。
│   │   // 可以修改，修改后会影响标签页的交互。
│   │   ├── timeline.js
│   │   // 时间线脚本。
│   │   // 可以修改，修改后会影响时间线的显示。
├── source/
│   // 静态资源文件夹，用于存储主题的 CSS、JS 和图片文件。
│   ├── css/
│   │   // CSS 文件夹，用于存储主题的样式文件。
│   │   ├── _global/
│   │   │   ├── function.styl
│   │   │   // 全局函数样式。
│   │   │   // 可以修改，修改后会影响全局样式的功能。
│   │   │   ├── index.styl
│   │   │   // 全局主样式。
│   │   │   // 可以修改，修改后会影响全局样式的显示。
│   │   ├── _highlight/
│   │   │   // 代码高亮样式。
│   │   │   ├── highlight/
│   │   │   │   ├── diff.styl
│   │   │   │   // Diff 代码高亮样式。
│   │   │   │   // 可以修改，修改后会影响 Diff 代码的显示。
│   │   │   │   ├── index.styl
│   │   │   │   // 代码高亮主样式。
│   │   │   │   // 可以修改，修改后会影响代码高亮的显示。
│   │   │   ├── prismjs/
│   │   │   │   ├── diff.styl
│   │   │   │   // Prism.js Diff 样式。
│   │   │   │   // 可以修改，修改后会影响 Prism.js Diff 代码的显示。
│   │   │   │   ├── index.styl
│   │   │   │   // Prism.js 主样式。
│   │   │   │   // 可以修改，修改后会影响 Prism.js 的显示。
│   │   │   │   ├── line-number.styl
│   │   │   │   // Prism.js 行号样式。
│   │   │   │   // 可以修改，修改后会影响 Prism.js 行号的显示。
│   │   │   ├── highlight.styl
│   │   │   // 代码高亮样式。
│   │   │   // 可以修改，修改后会影响代码高亮的显示。
│   │   │   ├── theme.styl
│   │   │   // 代码高亮主题样式。
│   │   │   // 可以修改，修改后会影响代码高亮主题的显示。
│   │   ├── _layout/
│   │   │   // 布局样式。
│   │   │   ├── aside.styl
│   │   │   // 侧边栏样式。
│   │   │   // 可以修改，修改后会影响侧边栏的显示。
│   │   │   ├── chat.styl
│   │   │   // 聊天样式。
│   │   │   // 可以修改，修改后会影响聊天功能的显示。
│   │   │   ├── comments.styl
│   │   │   // 评论样式。
│   │   │   // 可以修改，修改后会影响评论功能的显示。
│   │   │   ├── footer.styl
│   │   │   // 页脚样式。
│   │   │   // 可以修改，修改后会影响页脚的显示。
│   │   │   ├── head.styl
│   │   │   // 头部样式。
│   │   │   // 可以修改，修改后会影响头部的显示。
│   │   │   ├── loading.styl
│   │   │   // 加载样式。
│   │   │   // 可以修改，修改后会影响加载效果的显示。
│   │   │   ├── pagination.styl
│   │   │   // 分页样式。
│   │   │   // 可以修改，修改后会影响分页的显示。
│   │   │   ├── post.styl
│   │   │   // 文章样式。
│   │   │   // 可以修改，修改后会影响文章的显示。
│   │   │   ├── relatedposts.styl
│   │   │   // 相关文章样式。
│   │   │   // 可以修改，修改后会影响相关文章的显示。
│   │   │   ├── reward.styl
│   │   │   // 打赏样式。
│   │   │   // 可以修改，修改后会影响打赏功能的显示。
│   │   │   ├── rightside.styl
│   │   │   // 右侧边栏样式。
│   │   │   // 可以修改，修改后会影响右侧边栏的显示。
│   │   │   ├── sidebar.styl
│   │   │   // 侧边栏样式。
│   │   │   // 可以修改，修改后会影响侧边栏的显示。
│   │   │   ├── third-party.styl
│   │   │   // 第三方样式。
│   │   │   // 可以修改，修改后会影响第三方功能的显示。
│   │   ├── _mode/
│   │   │   // 模式样式。
│   │   │   ├── darkmode.styl
│   │   │   // 暗黑模式样式。
│   │   │   // 可以修改，修改后会影响暗黑模式的显示。
│   │   │   ├── readmode.styl
│   │   │   // 阅读模式样式。
│   │   │   // 可以修改，修改后会影响阅读模式的显示。
│   │   ├── _page/
│   │   │   // 页面样式。
│   │   │   ├── 404.styl
│   │   │   // 404 页面样式。
│   │   │   // 可以修改，修改后会影响 404 页面的显示。
│   │   │   ├── archives.styl
│   │   │   // 归档页面样式。
│   │   │   // 可以修改，修改后会影响归档页面的显示。
│   │   │   ├── categories.styl
│   │   │   // 分类页面样式。
│   │   │   // 可以修改，修改后会影响分类页面的显示。
│   │   │   ├── common.styl
│   │   │   // 公共页面样式。
│   │   │   // 可以修改，修改后会影响公共页面的显示。
│   │   │   ├── flink.styl
│   │   │   // 友链页面样式。
│   │   │   // 可以修改，修改后会影响友链页面的显示。
│   │   │   ├── homepage.styl
│   │   │   // 首页样式。
│   │   │   // 可以修改，修改后会影响首页的显示。
│   │   │   ├── shuoshuo.styl
│   │   │   // 说说页面样式。
│   │   │   // 可以修改，修改后会影响说说页面的显示。
│   │   │   ├── tags.styl
│   │   │   // 标签页面样式。
│   │   │   // 可以修改，修改后会影响标签页面的显示。
│   │   ├── _search/
│   │   │   // 搜索功能样式。
│   │   │   ├── algolia.styl
│   │   │   // Algolia 搜索功能样式。
│   │   │   // 可以修改，修改后会影响 Algolia 搜索功能的显示。
│   │   │   ├── index.styl
│   │   │   // 搜索功能主样式。
│   │   │   // 可以修改，修改后会影响搜索功能的显示。
│   │   │   ├── local-search.styl
│   │   │   // 本地搜索样式。
│   │   │   // 可以修改，修改后会影响本地搜索的显示。
│   │   ├── _tags/
│   │   │   // 标签样式。
│   │   │   ├── button.styl
│   │   │   // 按钮样式。
│   │   │   // 可以修改，修改后会影响按钮的显示。
│   │   │   ├── gallery.styl
│   │   │   // 图库样式。
│   │   │   // 可以修改，修改后会影响图库的显示。
│   │   │   ├── hexo.styl
│   │   │   // Hexo 样式。
│   │   │   // 可以修改，修改后会影响 Hexo 的显示。
│   │   │   ├── hide.styl
│   │   │   // 隐藏样式。
│   │   │   // 可以修改，修改后会影响隐藏功能的显示。
│   │   │   ├── inlinelmg.styl
│   │   │   // 内联图片样式。
│   │   │   // 可以修改，修改后会影响内联图片的显示。
│   │   │   ├── label.styl
│   │   │   // 标签样式。
│   │   │   // 可以修改，修改后会影响标签的显示。
│   │   │   ├── note.styl
│   │   │   // 笔记样式。
│   │   │   // 可以修改，修改后会影响笔记的显示。
│   │   │   ├── series.styl
│   │   │   // 系列样式。
│   │   │   // 可以修改，修改后会影响系列文章的显示。
│   │   │   ├── tabs.styl
│   │   │   // 标签页样式。
│   │   │   // 可以修改，修改后会影响标签页的显示。
│   │   │   ├── timeline.styl
│   │   │   // 时间线样式。
│   │   │   // 可以修改，修改后会影响时间线的显示。
│   │   ├── _third-party/
│   │   │   // 第三方样式。
│   │   │   ├── normalize.min.css
│   │   │   // Normalize CSS 样式。
│   │   │   // 一般不需要修改。
│   │   ├── index.styl
│   │   // 主样式文件。
│   │   // 可以修改，修改后会影响整体样式。
│   │   ├── var.styl
│   │   // 变量样式文件。
│   │   // 可以修改，修改后会影响样式的变量值。
│   ├── js/
│   │   // JavaScript 文件夹，用于存储主题的 JS 文件。
│   │   ├── search
│   │   │   ├── algolia.js
│   │   │   // Algolia 搜索功能 JS。
│   │   │   // 可以修改，修改后会影响 Algolia 搜索结果的显示。
│   │   │   ├── local-search.js
│   │   │   // 本地搜索 JS。
│   │   │   // 可以修改，修改后会影响本地搜索的功能。
│   │   ├── main.js
│   │   // 主 JS 文件。
│   │   // 可以修改，修改后会影响主题的 JS 功能。
│   │   ├── sakura.js
│   │   // Sakura 功能 JS。
│   │   // 可以修改，修改后会影响 Sakura 功能的显示。
│   │   ├── tw_cn.js
│   │   // 繁体中文 JS。
│   │   // 可以修改，修改后会影响繁体中文的显示。
│   │   ├── utils.js
│   │   // 工具 JS。
│   │   // 可以修改，修改后会影响工具功能的交互。
│   └── img/
│       // 图片文件夹，用于存储主题的图片资源。
│       // 可以修改，修改后会影响图片的显示。
```
