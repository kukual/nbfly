---
title: 利用Github和hexo搭建自己的个人博客
categories: 博客搭建
tags:
  - git
  - hexo
description: 该教程详细指导用户从零开始搭建Hexo博客并部署到GitHub。内容涵盖Git、Node.js环境安装，Hexo框架初始化，主题安装（以Amazing主题为例），以及GitHub仓库创建与SSH密钥配置。通过图文并茂的步骤演示了本地测试、主题配置、依赖安装和最终部署流程。重点解决了国内用户使用npm速度慢的问题（推荐cnpm），并提供了常见问题的解决方案，如环境变量配置和SSH认证测试，适合新手快速搭建个人技术博客。
top_img: /img/101.jpeg
cover: /img/102.jpeg
abbrlink: ec335aec
date: 2025-03-28 04:52:00
updated: 2025-03-28 04:52:11
swiper_index: 1
---
# 利用Github和hexo搭建自己的个人博客
## 1 安装Git
**官方地址**： https://git-scm.com/
1. 到Git官网下载与电脑操作系统对应的安装包，进行安装。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944483.png?imageSlim)
2. 安装步骤，，之后的步骤直接全部点击下一步，最后点击install。
选择安装路径，安装路径要全英文
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944484.png?imageSlim)
添加桌面快捷方式
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944485.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944486.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944487.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944488.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944489.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944490.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944491.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944492.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944493.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944494.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944495.png?imageSlim)
默认，点击下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944496.png?imageSlim)
等待安装
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944497.png?imageSlim)
最后这个界面就显示安装完成
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944498.png?imageSlim)
3. 安装好之后，在电脑桌面鼠标右键选择Open Git Bash Here，出现git窗口。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944499.png?imageSlim)
4. 输入：`git --version`，出现版本信息，说明安装成功。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944500.png?imageSlim)
## 2 安装node.js
**官方地址**： https://nodejs.org/en/download/
1. 到官网下载安装包，然后点击运行安装。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944501.png?imageSlim)
来到node.js安装界面
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944502.png?imageSlim)
点击同意
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944503.png?imageSlim)
更改路径
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944504.png?imageSlim)
下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944505.png?imageSlim)
下一步
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944506.png?imageSlim)
最后点击install。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944507.png?imageSlim)
等待安装
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944508.png?imageSlim)
显示安装成功，点击finish。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944509.png?imageSlim)
2. 安装好之后，配置环境变量
右键点击“此电脑”，点击属性。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944510.png?imageSlim)
点击高级系统设置
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944511.png?imageSlim)
点击环境变量
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944512.png?imageSlim)
在系统变量中点击新建
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944513.png?imageSlim)
填写变量名，变量值为node.js的安装路径。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944515.png?imageSlim)
最后点击确认就完成了环境变量的配置。
3. 在Git终端里面输入：`node -v`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944516.png?imageSlim)
出现版本号说明安装成功了。
## 3 安装hexo
### 3.1 安装cnpm
1. cnpm 是 中国版的 npm（Node Package Manager），解决国内用户访问官方 npm 仓库速度慢的问题。
2. 安装命令：
	`npm install -g cnpm --registry==https://registry.npm.taobao.org`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944517.png?imageSlim)
3. 测试命令：`cnpm -v`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944518.png?imageSlim)
出现版本号说明安装成功。
### 3.2 安装hexo
1. 安装命令：`cnpm install hexo-cli -g`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944519.png?imageSlim)
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944520.png?imageSlim)
2. 测试命令：`hexo -v`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944521.png?imageSlim)
出现这样的界面说明安装成功
## 4 hexo搭建本地博客测试
### 4.1 搭建博客
1. 新建一个Blogs的文件夹，进入文件夹，右键选择Open Git Bash Here，进入Git终端。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944522.png?imageSlim)
2. 初始化hexo命令：`hexo init`。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944523.png?imageSlim)
	初始化成功后，Blogs文件夹下出现许多文件
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944524.png?imageSlim)
3. 安装hexo相关依赖
	命令：`npm install`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944525.png?imageSlim)
	命令2：`npm install hexo-deployer-git --save`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944526.png?imageSlim)
4. 启动hexo命令：`hexo s`。先不要ctrl+c，不然就会停止服务
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944527.png?imageSlim)
5. 在浏览器访问 http://localhost:4000/ ,就可以看到hexo默认的页面。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944528.png?imageSlim)
### 4.2 修改主题
hexo主题官网： https://hexo.io/themes/
1. 选择amazing主题
	主题下载及安装教程： https://github.com/removeif/hexo-theme-amazing
	主题预览： https://dogzi.fun/
	下载主题的命令：`git clone https://github.com/removeif/hexo-theme-amazing.git themes/amazing`。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944529.png?imageSlim)
	ok,这样就下载好了。
	在Blogs的themes目录下就可以看到amazing主题文件夹。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944530.png?imageSlim)
2. 安装 semver 模块
命令：`npm install semver --save`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944531.png?imageSlim)
3. 安装缺失的依赖
命令：`npm install --save bulma-stylus@0.8.0 hexo-component-inferno@^3.1.2 hexo-renderer-inferno@^1.0.2 inferno@^8.2.3 inferno-create-element@^8.2.3`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944532.png?imageSlim)
4. 安装主题依赖
命令：`npm install hexo-renderer-pug hexo-renderer-stylus --save`。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944533.png?imageSlim)
5. 配置amazing主题
	以下步骤为个人主观配置，具体配置步骤请参考文章： https://github.com/removeif/hexo-theme-amazing 。
- 打开`D:\Blogs\_config.yml`文件， 找到theme部分，将landscape改为amazing。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944534.png?imageSlim)
- 在`D:\Blogs\amazing\`目录下创建`_config.amazing.yml`文件，把`\amazing\_config.yml`文件里面的内容复制到`_config.amazing.yml`文中。
- 后续修改博客的配置只需修改`_config.amazing.yml`文件。
### 4.3 预览主题
1. 使用`hexo clean`命令清除缓存
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944535.png?imageSlim)
2. 使用`hexo g`命令生成静态网页，生成 public 文件夹
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944536.png?imageSlim)
3. 使用`hexo s`命令启动hexo
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944537.png?imageSlim)
4. 在浏览器访问 http://localhost:4000/ ,就可以看到amazing主题的页面。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944538.png?imageSlim)
## 接下来就是将hexo部署到GitHub
## 5 git配置SSH key
可以免密的将本地的源码和资源上传到github，无需要每次都输账号和密码。
### 5.1 没有Github账号的，要先注册
### 5.2 生成ssh key
1. 命令：`ssh-keygen -t rsa -C "邮件地址"`
	- **注意**：邮箱地址为注册GitHub时使用的邮箱地址。
			输入命令后连续按三次回车。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944539.png?imageSlim)
2. 在用户文件夹下可以看到一个.ssh文件夹
	![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944540.png?imageSlim)
3. 进入文件夹，打开id_rsa.pub文件，复制里面的内容
### 5.3 添加ssh key到GitHub
1. 打开github主页，点击右上角个人头像，再点击Settings
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944541.png?imageSlim)
2. 进入到个人设置页面后，点击左侧的SSH and GPG keys选项，再点击New SSH key
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944542.png?imageSlim)
3. title自定义，key为id_rsa.pub文件复制的内容。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944543.png?imageSlim)
最后点击 Add SSH key
4. 测试是否添加成功
	命令：`ssh -T git@github.com`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944544.png?imageSlim)
出现`You've successfully authenticated, but GitHub does not provide shell access.`，说明添加成功。
5. 配置账号和密码
命令1：`git config --global user.name "yourname"`，yourname为GitHub用户名
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944545.png?imageSlim)
命令2：`git config --global user.email "youremail"`，youremail为GitHub注册邮箱
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944546.png?imageSlim)
## 6 搭建个人博客
### 6.1 创建博客文件夹
在`4 hexo搭建本地博客测试`中已经创建过了
### 6.2 创建仓库
1. 在右上角个人头像附近有个+，点它，然后再点New repository
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944547.png?imageSlim)
2. 给仓库命名，进行其他设置，点击创建
	仓库名称格式：用户名.github.io
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944548.png?imageSlim)
3. 打开`D:\Blogs\_config.yml`文件，拉到最后。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944549.png?imageSlim)
	找到deploy这部分，替换为以下内容：
```javascript
deploy:
  type: git
  repository: git@github.com:name/name.github.io.git 
  branch: main
```
name为GitHub用户名和仓库名，branch要看仓库是main还是master。
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944550.png?imageSlim)
修改后的
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944551.png?imageSlim)
### 6.3 发布到github 
1. 命令：`hexo d`
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944552.png?imageSlim)
	出现Deploy done: git，说明上传成功。
2. 在浏览器访问 https://kukual.github.io/
出现以下界面，说明访问成功
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250514143944553.png?imageSlim)
### 6.4 其他
hexo搭建博客详细教程请查看 https://hexo.io/zh-cn/docs/index.html