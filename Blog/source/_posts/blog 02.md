---
title: 腾讯云COS+Obsidian实现图片自动上传到图床
categories: 博客搭建
tags:
  - 图床
  - cos
  - obsidian
  - PicList
description: 文章介绍如何通过腾讯云COS和PicList工具实现Obsidian笔记的图片自动上传。步骤包括：腾讯云COS存储桶创建、API密钥获取、PicList安装与配置（含时间戳重命名防冲突），以及Obsidian插件Image Auto Upload的安装与设置。详细说明了手动/自动上传图片的操作方法，并配有多张界面截图，帮助用户无缝衔接本地写作与云端图床管理，提升Markdown文档的图片管理效率。
top_img: /img/103.jpeg
cover: /img/104.jpg
abbrlink: 77f87ebd
date: 2025-03-29 04:52:00
updated: 2025-03-29 04:52:00
swiper_index: 2
---
# 腾讯云COS+Obsidian实现图片自动上传到图床
可参考使用教程： https://piclist.cn/app.html
## 1 腾讯云cos
注册腾讯云，创建cos，创建api密钥。详细操作步骤请自行查找相关资料。
## 2 安装配置PicList
图床管理工具我选了picgo，而piclist又是基于picgo的最新版本，最终选择安装piclist。
1. PicGo下载地址
	https://github.com/Molunerfinn/PicGo
	https://molunerfinn.com/PicGo/
2. PicList安装步骤
	官网： https://piclist.cn/
	安装步骤过程：
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842153.png?imageSlim)
	选择安装位置
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842154.png?imageSlim)
	等待安装
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842155.png?imageSlim)
	安装完成
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842156.png?imageSlim)
	软件打开后的界面
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842157.png?imageSlim)
3. 配置PicList
	详细配置教程请看 https://piclist.cn/configure.html#%E8%85%BE%E8%AE%AF%E4%BA%91cos
	打开PicList图床设置，选择腾讯云COS，点击编辑按钮
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842158.png?imageSlim)
	根据要求，进行相应配置
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842159.png?imageSlim)
	点击导入，再点确认，完成设置。
	最后点击设为默认图床。
	进入设置-上传设置，打开时间戳重命名，以防止文件名冲突。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842160.png?imageSlim)
# 3 Obsidian安装插件
安装Image Auto Upload Plugin插件 
打开 Obsidian，点击设置，选择第三方插件，关闭安全模式然后打开浏览插件市场进行搜索安装。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842161.png?imageSlim)
点击安装
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842162.png?imageSlim)
点击启用
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842163.png?imageSlim)
点击选项
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842164.png?imageSlim)
进入插件设置，修改默认上传器为 PicGo(app)， 此外该插件还额外支持通过PicList进行云端删除，其他设置按需要来设置。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842165.png?imageSlim)
# 4 上传图片操作
1. 手动上传方法1：
	在文章中选择图片右键，选择upload就会上传。上传成功后会替换原图片
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842166.png?imageSlim)
2. 手动上传方法2：
	打开一篇笔记，按下ctrl+p唤出命令行，输入upload，选择上传图片，可以上传这篇笔记的所有图片到图床。上传完成后会替换原图片
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842167.png?imageSlim)
3. 自动上传设置
	在插件设置中打开剪切板自动上传
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509155842168.png?imageSlim)