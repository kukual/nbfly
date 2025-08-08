---
title: butterfly主题魔改10：分类页面魔改
categories: 博客搭建
tags:
  - hexo
  - butterfly
description: >-
  本文指导用户通过插件hexo-butterfly-categories-card改造分类页面。安装插件后，新建CSS文件并修改插件的JavaScript与Pug模板，实现瀑布流式分类卡片布局。卡片支持背景图动态缩放、悬停文字平移特效，并适配移动端响应式设计。配置文件定义分类卡片的列数、行数、封面图及描述信息，最终生成高交互性的分类导航页。修改后的分类页面以视觉化的卡片形式展示分类名称、文章数量及简介，大幅提升内容呈现的层次感与吸引力。
top_img: /img/125.jpeg
cover: /img/126.jpeg
abbrlink: a7bebfb0
date: 2025-04-09 04:52:00
updated: 2025-04-09 04:52:00
swiper_index:
---
# butterfly主题魔改10：分类页面魔改
参考 https://akilar.top/posts/a9131002/
## 效果图
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509161040933.png?imageSlim)
## 01 安装插件
安装命令
```bash
npm install hexo-butterfly-categories-card --save
```
## 02 新建样式文件
在博客根目录`themes\butterfly\source\css\`下新建`categorybar.css`文件，添加 https://npm.elemecdn.com/hexo-butterfly-categories-card@1.0.0/lib/categorybar.css 的代码。
```css
#categoryBar {
  width: 100% !important;
}
ul.categoryBar-list {
  margin: 5px 5px 0 5px !important;
  padding: 0 !important;
}
li.categoryBar-list-item {
  font-weight: bold;
  display: inline-block;
  height: 180px !important;
  margin: 5px 0.5% 0 0.5% !important;
  background-image: linear-gradient(rgba(0,0,0,0.4) 25%, rgba(16,16,16,0) 100%);
  border-radius: 10px;
  padding: 25px 0 25px 25px !important;
  box-shadow: rgba(50,50,50,0.3) 50px 50px 50px 50px inset;
  overflow: hidden;
  background-size: 100% !important;
  background-position: center !important;
}
li.categoryBar-list-item:hover {
  background-size: 110% !important;
  box-shadow: inset 500px 50px 50px 50px rgba(50,50,50,0.6);
}
li.categoryBar-list-item:hover span.categoryBar-list-descr {
  transition: all 0.5s;
  transform: translate(-100%, 0);
}
a.categoryBar-list-link {
  color: #fff !important;
  font-size: 20px !important;
}
a.categoryBar-list-link::before {
  content: '|' !important;
  color: #fff !important;
  font-size: 20px !important;
}
a.categoryBar-list-link:after {
  content: '';
  position: relative;
  width: 0;
  bottom: 0;
  display: block;
  height: 3px;
  border-radius: 3px;
  background-color: #fff;
}
a.categoryBar-list-link:hover:after {
  width: 90%;
  left: 1%;
  transition: all 0.5s;
}
span.categoryBar-list-count {
  display: block !important;
  color: #fff !important;
  font-size: 20px !important;
}
span.categoryBar-list-count::before {
  content: '\f02d' !important;
  padding-right: 15px !important;
  display: inline-block;
  font-weight: 600;
  font-style: normal;
  font-variant: normal;
  font-family: 'Font Awesome 6 Free';
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
}
span.categoryBar-list-descr {
  padding: 5px;
  display: block !important;
  color: #fff !important;
  font-size: 20px !important;
  position: relative;
  right: -100%;
}
@media screen and (max-width: 650px) {
  li.categoryBar-list-item {
    width: 48% !important;
    height: 150px !important;
    margin: 5px 1% 0 1% !important;
  }
}

```
## 03 修改插件js样式文件
打开博客根目录下`node_modules\hexo-butterfly-categories-card\index.js`文件，全部替换成以下代码：
```js
'use strict'
// 全局声明插件代号
const pluginname = 'butterfly_categories_card'
// 全局声明依赖
const pug = require('pug')
const path = require('path')
const urlFor = require('hexo-util').url_for.bind(hexo)
const util = require('hexo-util')

hexo.extend.filter.register('after_generate', function () {

// =====================================================================
  // 首先获取整体的配置项名称
  const config = hexo.config.categoryBar || hexo.theme.config.categoryBar
  // 如果配置开启
  if (!(config && config.enable)) return
    // 获取所有分类
    var categories_list= hexo.locals.get('categories').data;
    var categories_message= config.message;
    //声明一个空数组用来存放合并后的对象
    var new_categories_list = [];
    // 合并分类属性和新添加的封面描述属性
    // 合并分类属性和新添加的封面描述属性
    for (var i = 0; i < categories_list.length; i++) {
      var a = categories_list[i];
      var b = categories_message[i];
      // 确保不覆盖原分类路径
      new_categories_list[i] = Object.assign({}, a, { path: a.path }, b);
    }
    // console.log(new_categories_list)
  // 集体声明配置项
    const data = {
      pjaxenable: hexo.theme.config.pjax.enable,
      enable_page: config.enable_page ? config.enable_page : "/",
      layout_type: config.layout.type,
      layout_name: config.layout.name,
      layout_index: config.layout.index ? config.layout.index : 0,
      categories_list: new_categories_list,
      column: config.column ? config.column : odd, // odd：3列 | even：4列
      row: config.row ? config.row : 2, //显示行数，默认两行，超过行数切换为滚动显示
      custom_css: config.custom_css ? urlFor(config.custom_css) : "https://cdn.jsdelivr.net/npm/hexo-butterfly-categories-card/lib/categorybar.css"
    }
  // 渲染页面
  const temple_html_text = config.temple_html ? config.temple_html : pug.renderFile(path.join(__dirname, './lib/html.pug'),data);

  //cdn资源声明
    //样式资源
  const css_text = `<link rel="stylesheet" href="${data.custom_css}">`
  //注入容器声明
  var get_layout
  //若指定为class类型的容器
  if (data.layout_type === 'class') {
    //则根据class类名及序列获取容器
    get_layout = `document.getElementsByClassName('${data.layout_name}')[${data.layout_index}]`
  }
  // 若指定为id类型的容器
  else if (data.layout_type === 'id') {
    // 直接根据id获取容器
    get_layout = `document.getElementById('${data.layout_name}')`
  }
  // 若未指定容器类型，默认使用id查询
  else {
    get_layout = `document.getElementById('${data.layout_name}')`
  }

  //挂载容器脚本
  //挂载容器脚本（动态创建容器）
  var user_info_js = `<script data-pjax>
  function ${pluginname}_injector_config(){
    // 检查容器是否存在
    var parent_div_git = ${get_layout};
    // 如果容器不存在，则动态创建
    if (!parent_div_git) {
      console.warn('${pluginname}: 挂载容器不存在，正在动态创建...');
      // 创建新容器（默认插入到页面主体顶部）
      parent_div_git = document.createElement('div');
      parent_div_git.id = '${data.layout_name}'; // 赋予配置的ID
      document.querySelector('#page').prepend(parent_div_git); // 插入到 #content-inner 内
    }
    var item_html = '${temple_html_text}';
    console.log('已挂载 ${pluginname}');
    parent_div_git.insertAdjacentHTML("afterbegin",item_html)
  }
  // 路径匹配逻辑（使用 startsWith）
  if (location.pathname.startsWith('${data.enable_page}') || '${data.enable_page}' === 'all') {
    ${pluginname}_injector_config();
  }
  </script>`
  // 注入用户脚本
  // 此处利用挂载容器实现了二级注入
  hexo.extend.injector.register('body_end', user_info_js, "default");
  // 注入样式资源
  hexo.extend.injector.register('head_end', css_text, "default");
},
hexo.extend.helper.register('priority', function(){
  // 过滤器优先级，priority 值越低，过滤器会越早执行，默认priority是10
  const pre_priority = hexo.config.categoryBar.priority || hexo.theme.config.categoryBar.priority
  const priority = pre_priority ? pre_priority : 10
  return priority
})
)

```
## 04 修改插件html.pug文件
打开博客根目录下`node_modules\hexo-butterfly-categories-card\lib\html.pug`文件，全部替换成以下代码：
```Pu
- var prow = 190 * row + 'px'
- var mrow = 160 * row + 'px'

if (column === 'odd')
  style.
    li.categoryBar-list-item{width:32.3%;}.categoryBar-list{max-height: #{prow};overflow:auto;}.categoryBar-list::-webkit-scrollbar{width:0!important}@media screen and (max-width: 650px){.categoryBar-list{max-height: #{mrow};}}
else if (column === 'even')
  style.
    li.categoryBar-list-item{width:24%;}.categoryBar-list{max-height: #{prow};overflow:auto;}.categoryBar-list::-webkit-scrollbar{width:0!important}@media screen and (max-width: 650px){.categoryBar-list{max-height: #{mrow};}}
.recent-post-item(style='height:auto;width:100%;padding:0px;')
  #categoryBar
    ul.categoryBar-list
      if pjaxenable
        each cl in categories_list
          li.categoryBar-list-item(style=`background:url(` + cl.cover + `);`)  
            //- 强制修正路径：移除重复的 categories 前缀
            - var cleanPath = cl.path.replace(/^\/?categories\//, '')
            a.categoryBar-list-link(
              onclick=`pjax.loadUrl("/categories/${cleanPath}");`
              href='javascript:void(0);'
            )= cl.name
            span.categoryBar-list-count= cl.length
            span.categoryBar-list-descr= cl.descr
      else
        each cl in categories_list
          li.categoryBar-list-item(style=`background:url(` + cl.cover + `);`)  
            //- 直接输出修正后的路径
            - var cleanPath = cl.path.replace(/^\/?categories\//, '')
            a.categoryBar-list-link(href=`/categories/${cleanPath}`)= cl.name
            span.categoryBar-list-count= cl.length
            span.categoryBar-list-descr= cl.descr
```
## 05 修改配置文件
在博客根目录下`_config.butterfly.yml`文件添加以下代码：
```yaml
# hexo-butterfly-categories-card
# see https://akilar.top/posts/a9131002/
categoryBar:
  enable: true # 开关
  priority: 5 #过滤器优先权
  enable_page: /categories/ # 应用页面
  layout: # 挂载容器类型
    type: id
    name: recent-posts
    index: 0
  column: odd # odd：3列 | even：4列
  row: 5 #显示行数，默认两行，超过行数切换为滚动显示
  message:
    - descr: 1
      cover: /img/11.png
    - descr: 2
      cover: /img/12.png
    - descr: 3
      cover: /img/13.png
    - descr: 4
      cover: /img/14.png
    - descr: 5
      cover: /img/15.png
    - descr: 6
      cover: /img/16.png
    - descr: 7
      cover: /img/17.png
    - descr: 8
      cover: /img/18.png
  custom_css: /css/categorybar.css
```

