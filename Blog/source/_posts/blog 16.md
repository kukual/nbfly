---
title: " butterfly主题魔改13：关于页面美化（手搓）"
categories: 博客搭建
tags:
  - hexo
  - butterfly
description: 这篇文章将带你深入了解如何通过纯手工的方式美化你的“关于”页面。从创建页面文件到编写自定义的HTML和CSS代码，作者展示了如何打造一个充满个性和视觉吸引力的“关于”页面。文章中不仅提供了详细的代码示例，还展示了如何通过自定义样式和动画效果，让你的页面在众多站点中脱颖而出。无论你是前端开发者还是设计爱好者，这篇文章都将为你提供丰富的灵感和实用的技巧。
top_img:
  - /img/131.jpeg
cover:
  - /img/132.jpeg
abbrlink: 4be26d1b
date: 2025-04-12 04:52:00
updated: 2025-04-12 04:52:00
swiper_index:
---
# butterfly主题魔改13：关于页面美化（手搓）
## 01 效果图
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509161209279.gif?imageSlim)
## 02 创建页面
在博客根目录的`source`文件夹下创建`about`文件夹，在文件夹`about`下创建`index.md`文件，写入以下代码：

```html
---
title: kukual的自述
date: 2025-05-03 01:22:00 
aside: false 
type: about 
---
<style>
    :root {
        --main-color: #6a0dad;
        --secondary-color: #8a2be2;
        --accent-color: #9932cc;
        font-family: 'Comic Neue', 'Noto Sans SC', cursive;
        --text-color: #d7b8ff;
        --dark-purple: #2d0a3d;
        --bg-gradient: linear-gradient(135deg, var(--dark-purple) 0%, #4b0082 100%);
        --card-bg: rgba(45, 10, 61, 0.7);
        --glow-effect: 0 0 10px rgba(154, 50, 204, 0.7), 0 0 20px rgba(154, 50, 204, 0.5);
    }
    body {
        color: var(--text-color);
        font-family: 'Noto Sans SC', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        line-height: 1.8;
        margin: 0;
        padding: 0;
        min-height: 100vh;
        overflow-x: hidden;
        background-attachment: fixed;
        background-size: cover;
    }
    #page {
    	background: linear-gradient(135deg, #2d0a3d99 0%, #4b008299 100%) !important;
    }
    p {
        font-size: 1.35rem;
        font-family: 'Ma Shan Zheng', cursive;
        line-height: 1.6;
        color: var(--text-color);
        font-weight: 400;
        text-shadow: 0 0 5px rgba(154, 50, 204, 0.2);
    }
    .header {
        text-align: center;
        margin-bottom: 2rem;
        position: relative;
        z-index: 1;
    }
    .header::after {
        content: "";
        display: block;
        width: 100%;
        height: 4px;
        background: linear-gradient(to right, transparent, var(--accent-color), transparent);
        margin: 1rem auto;
        border-radius: 60%;
        box-shadow: var(--glow-effect);
    }
    .header h1 {
        font-size: 7rem;
        font-family: 'Fredoka One';
        line-height: 0.7;
        color: var(--secondary-color);
        margin-bottom: 2rem;
        text-shadow: 8px 8px 16px rgba(0, 0, 0, 0.3), 0 0 40px rgba(138, 43, 226, 0.5);
        font-weight: 800;
        letter-spacing: 2px;
        font-family: 'ZCOOL KuaiLe', cursive;
        position: relative;
        display: inline-block;
        background: linear-gradient(to bottom, #6a0dad, #9b30ff);
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
    }
    .header h1::after {
        content: "";
        position: absolute;
        bottom: -15px;
        left: 50%;
        transform: translateX(-50%);
        width: 100%;
        height: 3px;
        background: linear-gradient(90deg, transparent, #6a0dad, transparent);
        border-radius: 10px;
    }
    h2 {
        font-size: 2rem;
        color: var(--secondary-color);
        margin-bottom: 2rem;
        font-family: 'ZCOOL KuaiLe', cursive;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        padding-bottom: 10px;
        gap: 1rem;
    }
    h2::before {
        content: "\f0e7";
        font-family: "Font Awesome 6 Free";
        font-weight: 700;
        color: var(--accent-color);
    }
    h2::after {
        content: "\f0e7";
        font-family: "Font Awesome 6 Free";
        font-weight: 700;
        color: var(--accent-color);
    }
    h2 .underline {
        position: absolute;
        bottom: 0;
        left: 50%;
        transform: translateX(-50%);
        width: 100%;
        height: 3px;
        background: linear-gradient(90deg, transparent, #6a0dad, transparent);
        border-radius: 10px;
    }
    .profile {
        display: flex;
        align-items: center;
        gap: 2rem;
        margin: 0rem 7rem;
        margin-bottom: 2rem;
        flex-wrap: wrap;
        position: relative;
        z-index: 1;
    }
    .avatar {
        width: 120px;
        height: 120px;
        border-radius: 50%;
        border: 4px solid var(--secondary-color);
        box-shadow: 0 0 20px rgba(138, 43, 226, 0.7);
        background: url('/img/02.jpg') no-repeat center center;
        background-size: cover;
        transition: all 0.3s ease;
        position: relative;
        overflow: hidden;
    }
    .avatar::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: radial-gradient(circle, transparent 60%, rgba(138, 43, 226, 0.3) 100%);
    }
    .avatar:hover {
        transform: rotate(5deg) scale(1.05);
        box-shadow: 0 0 30px rgba(138, 43, 226, 0.9);
    }
    .quote {
        flex: 1;
        font-style: italic;
        padding: 2rem;
        background: rgba(106, 13, 173, 0.15);
        border-right: 8px solid var(--accent-color);
        border-left: 8px solid var(--accent-color);
        position: relative;
        border-radius: 15px;
        transition: all 0.3s ease;
        box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.2);
        font-family: 'Caveat', cursive, 'Noto Sans SC', sans-serif;
        font-size: 1rem;
        font-weight: 600;
        line-height: 1.5;
    }
    .quote:hover {
        background: rgba(106, 13, 173, 0.25);
        transform: translateY(-3px);
        box-shadow: 0 5px 15px rgba(154, 50, 204, 0.3), inset 0 0 10px rgba(0, 0, 0, 0.2);
    }
    .quote::before {
        content: "\201C";
        font-size: 4rem;
        color: rgba(138, 43, 226, 0.8);
        position: absolute;
        top: -1rem;
        left: 0rem;
        font-family: serif;
    }
    .quote::after {
        content: "\201D";
        font-size: 4rem;
        color: rgba(138, 43, 226, 0.8);
        position: absolute;
        bottom: -3rem;
        right: 0.5rem;
        font-family: serif;
    }
    .bio {
        margin-bottom: 2.5rem;
        padding: 0 2rem 2rem 2rem;
        background: var(--card-bg);
        margin: 2rem 2rem;
        border-radius: 50px;
        position: relative;
        overflow: hidden;
        transition: all 0.3s ease;
        border-left: 12px solid rgba(167, 79, 238);
        border-right: 12px solid rgba(167, 79, 238);
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    }
    .bio:hover {
        background: rgba(106, 13, 173, 0.25);
        transform: translateY(-3px);
        box-shadow: 0 5px 15px rgba(154, 50, 204, 0.3);
    }
    .bio::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(135deg, transparent 0%, rgba(138, 43, 226, 0.05) 100%);
        pointer-events: none;
    }
    .bio p {
        font-size: 1.3rem;
        line-height: 1.8;
        color: #d880e4;
        font-weight: 500;
        margin: 2rem 2rem;
    }
    .section {
        margin-bottom: 2.5rem;
        padding: 0 2rem 2rem 2rem;
        background: var(--card-bg);
        border-radius: 15px;
        position: relative;
        overflow: hidden;
        transition: all 0.3s ease;
        border: 1px solid rgba(138, 43, 226, 0.3);
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    }
    .section:hover {
        transform: translateY(-5px);
        box-shadow: 0 10px 25px rgba(154, 50, 204, 0.4);
    }
    .section::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        width: 8px;
        height: 100%;
        background: linear-gradient(to bottom, var(--main-color), var(--secondary-color));
    }
    ul {
        list-style-type: none;
        padding-left: 25%;
    }
    li {
        position: relative;
        font-size: 1rem;
        color: #f29afd;
        font-weight: 300;
        padding-left: 1.5rem;
        margin-bottom: 0.5rem;
        transition: all 0.3s ease;
    }
    li:hover {
        transform: translateX(5px);
        color: var(--secondary-color);
    }
    li::before {
        content: "\f054";
        font-family: "Font Awesome 6 Free";
        font-weight: 1000;
        position: absolute;
        left: 0;
        color: #ca6fff;
        transition: all 0.3s ease;
    }
    li:hover::before {
        color: var(--secondary-color);
        transform: translateX(5px);
    }
    .skills {
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
        margin-top: 1rem;
    }
    .skill {
        padding: 0.5rem 1rem;
        background: rgba(138, 43, 226, 0.2);
        border: 2px dashed var(--accent-color);
        border-radius: 20px;
        font-size: 1rem;
        transition: all 0.3s ease;
        cursor: default;
        position: relative;
        overflow: hidden;
        font-family: 'Noto Sans SC', sans-serif;
        font-weight: 400;
    }
    .skill:hover {
        background: rgba(154, 50, 204, 0.4);
        transform: translateY(-3px);
        box-shadow: 0 5px 15px rgba(154, 50, 204, 0.3);
    }
    .skill-meter {
        width: 100%;
        background-color: rgba(138, 43, 226, 0.1);
        border-radius: 10px;
        margin: 0.5rem 0;
        overflow: hidden;
    }
    .skill-level {
        height: 8px;
        border-radius: 10px;
        background: linear-gradient(to right, var(--main-color), var(--secondary-color));
        box-shadow: 0 0 5px rgba(138, 43, 226, 0.5);
        transition: width 1s ease-in-out;
    }
    .project-card {
        background: rgba(224, 156, 255, 0.2);
        border-radius: 8px;
        padding: 1rem;
        margin-bottom: 1rem;
        border-left: 3px solid var(--accent-color);
        transition: all 0.3s ease;
    }
    .project-card:hover {
        transform: translateX(5px);
        background: rgba(45, 10, 61, 0.8);
    }
    .project-title {
        font-weight: bold;
        color: var(--secondary-color);
        margin-bottom: 0.5rem;
    }
    .project-desc {
        font-size: 0.9rem;
        margin-bottom: 0.5rem;
        font-family: 'Noto Sans SC', sans-serif;
        font-weight: 300;
        color: #e0c4ff;
        letter-spacing: 0.05em;
    }
    .project-tags {
        display: flex;
        flex-wrap: wrap;
        gap: 0.5rem;
    }
    .project-tag {
        background: rgba(138, 43, 226, 0.2);
        padding: 0.2rem 0.5rem;
        border-radius: 10px;
        font-size: 0.7rem;
    }
    .anime-list {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
        gap: 1.5rem;
        margin-top: 1.5rem;
    }
    .anime-card {
        background: rgba(45, 10, 61, 0.8);
        border-radius: 10px;
        overflow: hidden;
        transition: all 0.3s ease;
        border: 1px solid var(--main-color);
        position: relative;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    }
    .anime-card:hover {
        transform: translateY(-5px) scale(1.03);
        box-shadow: 0 10px 25px rgba(154, 50, 204, 0.5);
        z-index: 2;
    }
    .anime-card::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(to bottom, transparent 60%, rgba(0, 0, 0, 0.7) 100%);
        z-index: 1;
    }
    .anime-cover {
        height: 120px;
        background-size: cover;
        background-position: center;
        transition: all 0.5s ease;
        position: relative;
    }
    .anime-card:hover .anime-cover {
        transform: scale(1.1);
    }
    .anime-info {
        padding: 1rem;
        position: relative;
        z-index: 2;
        background: linear-gradient(to top, rgba(45, 10, 61, 0.9) 0%, transparent 100%);
    }
    .anime-title {
        font-weight: 800;
        font-size: 1.1rem;
        margin-bottom: 0.5rem;
        color: var(--secondary-color);
        text-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
    }
    .anime-genre {
        font-size: 0.8rem;
        color: var(--accent-color);
    }
    .floating-icons {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
    .floating-icon {
        position: absolute;
        color: rgba(138, 43, 226, 0.1);
        font-size: 1.5rem;
        animation: float linear infinite;
    }
    @keyframes float {
        0% {
            transform: translateY(0) rotate(0deg);
            opacity: 0;
        }
        10% {
            opacity: 0.1;
        }
        50% {
            opacity: 0.3;
        }
        100% {
            transform: translateY(-100vh) rotate(360deg);
            opacity: 0;
        }
    }
    @media (max-width: 768px) {
        .container {
            padding: 1rem;
        }
        h1 {
            font-size: 2.5rem;
        }
        .profile {
            flex-direction: column;
            text-align: center;
        }
        .bio {
            border-left: none;
            border-top: 3px solid var(--accent-color);
            border-radius: 0 0 10px 10px;
        }
        .anime-list {
            grid-template-columns: 1fr;
        }
    }
</style>
<div class="floating-icons" id="floatingIcons"></div>
<div class="container">
        <div class="header">
            <h1>kukualのblog</h1>
            <p style="font-size: 1.9rem; font-weight: 800; color: var(--accent-color); text-shadow: 0 0 10px rgba(154, 50, 204, 0.5);">「酷库阿洛」的网络安全研习录</p>
        </div>
        <div class="profile">
            <div class="quote">
                在代码的世界里寻找漏洞，在动漫的宇宙中寻找感动。技术是我的剑，动漫是我的盾，两者共同构筑我的数字生活。
            </div>
            <div class="avatar"></div>
        </div>
        <div class="bio">
            <h2>
                <span>关于我</span>
                <span class="underline"></span>
            </h2>
            <p>
                &nbsp;&nbsp;&nbsp;&nbsp;嗨！我是kukual，一名热爱网络安全的大三学生。白天是代码审计的学徒，夜晚是CTF赛场的战士。<br>
                &nbsp;&nbsp;&nbsp;&nbsp;我的技术之旅始于高中时期的一次校园网络安全比赛，从此便沉迷于二进制世界的神秘与挑战。<br>
                &nbsp;&nbsp;&nbsp;&nbsp;除了钻研安全技术，我也是一名狂热的动漫爱好者，尤其喜欢《名侦探柯南》、《黑子的篮球》这类侦探与运动热血的作品。
            </p>
            <div style="margin-top: 1rem; text-align: center;">
                <i class="fas fa-graduation-cap" style="color: var(--accent-color);"></i> &nbsp;&nbsp;某大学网络安全专业&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                <i class="fas fa-map-marker-alt" style="color: var(--accent-color);"></i>&nbsp;&nbsp;中国&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                <i class="fas fa-heart" style="color: var(--accent-color);"></i> &nbsp;&nbsp;网络安全 | 动漫 | 编程
            </div>
        </div>
        <div class="section">
            <h2>
                <span>博客内容</span>
                <span class="underline"></span>
            </h2>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 1rem;">
                <ul>
                    <li>网络安全技术研究与实战案例</li>
                    <li>CTF竞赛解题思路与技巧</li>
                    <li>漏洞复现与分析报告</li>
                    <li>安全工具使用与开发经验</li>
                </ul>
                <ul>
                    <li>偶尔的动漫推荐与感想</li>
                    <li>学习笔记与资源分享</li>
                    <li>技术书籍阅读心得</li>
                    <li>编程技巧与开发经验</li>
                </ul>
            </div>
        </div>
        <div class="section">
            <h2>
                <span>技术专长</span>
                <span class="underline"></span>
            </h2>
            <p style="font-size: 1.2rem; font-weight: 800; color: var(--accent-color); ">
                专注于网络安全技术研究，特别是渗透测试和漏洞分析领域。<br>
                以下是我正在深入研究的技能方向：
            </p>
            <div class="skills">
                <div class="skill"><i class="fas fa-shield-alt"></i> &nbsp;&nbsp;渗透测试</div>
                <div class="skill"><i class="fas fa-bug"></i> &nbsp;&nbsp;漏洞分析</div>
                <div class="skill"><i class="fas fa-trophy"></i> &nbsp;&nbsp;CTF竞赛</div>
                <div class="skill"><i class="fas fa-code"></i> &nbsp;&nbsp;安全开发</div>
                <div class="skill"><i class="fas fa-lock"></i> &nbsp;&nbsp;逆向工程</div>
                <div class="skill"><i class="fas fa-network-wired"></i> &nbsp;&nbsp;网络防御</div>
                <div class="skill"><i class="fas fa-tools"></i> &nbsp;&nbsp;安全工具</div>
                <div class="skill"><i class="fas fa-file-code"></i> &nbsp;&nbsp;代码审计</div>
                <div class="skill"><i class="fas fa-database"></i> &nbsp;&nbsp;Web安全</div>
                <div class="skill"><i class="fas fa-terminal"></i> &nbsp;&nbsp;Linux安全</div>
            </div>
            <h2 style="margin-top: 1.5rem;">
                <span>技能熟练度</span>
                <span class="underline"></span>
            </h2>
            <div>
                <p>Python <span style="float: right;">80%</span></p>
                <div class="skill-meter">
                    <div class="skill-level" style="width: 80%;"></div>
                </div>
                <p>渗透测试 <span style="float: right;">75%</span></p>
                <div class="skill-meter">
                    <div class="skill-level" style="width: 75%;"></div>
                </div>
                <p>Web安全 <span style="float: right;">70%</span></p>
                <div class="skill-meter">
                    <div class="skill-level" style="width: 70%;"></div>
                </div>
                <p>逆向工程 <span style="float: right;">65%</span></p>
                <div class="skill-meter">
                    <div class="skill-level" style="width: 65%;"></div>
                </div>
            </div>
        </div>
        <div class="section">
            <h2>
                <span>近期项目</span>
                <span class="underline"></span>
            </h2>
            <div class="project-card">
                <div class="project-title">Web漏洞扫描器开发</div>
                <div class="project-desc">基于Python开发的自动化Web漏洞扫描工具，支持XSS、SQL注入等常见漏洞检测。</div>
                <div class="project-tags">
                    <span class="project-tag">Python</span>
                    <span class="project-tag">Web安全</span>
                    <span class="project-tag">自动化</span>
                </div>
            </div>
            <div class="project-card">
                <div class="project-title">CTF解题工具集</div>
                <div class="project-desc">收集整理的CTF竞赛常用解题脚本和工具，涵盖密码学、逆向、PWN等多个方向。</div>
                <div class="project-tags">
                    <span class="project-tag">CTF</span>
                    <span class="project-tag">工具集</span>
                    <span class="project-tag">脚本</span>
                </div>
            </div>
            <div class="project-card">
                <div class="project-title">漏洞复现笔记</div>
                <div class="project-desc">记录常见漏洞的复现过程和分析报告，包括CVE漏洞和实际案例。</div>
                <div class="project-tags">
                    <span class="project-tag">漏洞分析</span>
                    <span class="project-tag">CVE</span>
                    <span class="project-tag">安全研究</span>
                </div>
            </div>
        </div>
        <div class="section">
            <h2>
                <span>近期追番</span>
                <span class="underline"></span>
            </h2>
            <p style="font-size: 1.2rem; font-weight: 800; color: var(--accent-color); ">作为一名资深动漫爱好者，这些是我最近在追或特别推荐的番剧：</p>
            <div class="anime-list">
                <div class="anime-card" herf="https://www.bilibili.com/bangumi/play/ep29721">
                    <div class="anime-cover" style="background-image: url('/img/51.jpg');"></div>
                    <div class="anime-info">
                        <div class="anime-title">黑子的篮球</div>
                        <div class="anime-genre">运动 / 热血 / 声控 / 社团</div>
                    </div>
                </div>
                <div class="anime-card" herf="https://www.bilibili.com/bangumi/play/ss34430">
                    <div class="anime-cover" style="background-image: url('/img/52.jpg');"></div>
                    <div class="anime-info">
                        <div class="anime-title">咒术回战</div>
                        <div class="anime-genre">动作 / 超自然 / 校园</div>
                    </div>
                </div>
                <div class="anime-card" herf="https://www.bilibili.com/bangumi/play/ss41410">
                    <div class="anime-cover" style="background-image: url('/img/53.png');"></div>
                    <div class="anime-info">
                        <div class="anime-title">间谍过家家</div>
                        <div class="anime-genre">喜剧 / 动作 / 家庭</div>
                    </div>
                </div>
                <div class="anime-card" herf="https://www.bilibili.com/bangumi/play/ss33378">
                    <div class="anime-cover" style="background-image: url('/img/54.jpg');"></div>
                    <div class="anime-info">
                        <div class="anime-title">名侦探柯南</div>
                        <div class="anime-genre">漫画改 / 推理 / 智斗 / 悬疑</div>
                    </div>
                </div>
                <div class="anime-card" herf="https://www.bilibili.com/bangumi/play/ss43164">
                    <div class="anime-cover" style="background-image: url('/img/55.jpg');"></div>
                    <div class="anime-info">
                        <div class="anime-title">孤独摇滚</div>
                        <div class="anime-genre">音乐 / 校园 / 喜剧</div>
                    </div>
                </div>
                <div class="anime-card" herf="https://www.bilibili.com/bangumi/play/ss26193">
                    <div class="anime-cover" style="background-image: url('/img/56.png');"></div>
                    <div class="anime-info">
                        <div class="anime-title">百妖谱</div>
                        <div class="anime-genre">漫改 / 古风 / 剧情</div>
                    </div>
                </div>
            </div>
        </div>
        <div class="section">
            <h2>
                <span>学习资源推荐</span>
                <span class="underline"></span>
            </h2>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 1rem;">
                <ul>
                    <li><a href="https://ctf-wiki.org/" style="color: var(--accent-color); text-decoration: none;">CTF Wiki</a> - 全面的CTF知识库</li>
                    <li><a href="https://www.hackthebox.com/" style="color: var(--accent-color); text-decoration: none;">Hack The Box</a> - 在线渗透测试练习平台</li>
                    <li><a href="https://www.vulnhub.com/" style="color: var(--accent-color); text-decoration: none;">VulnHub</a> - 漏洞环境下载</li>
                </ul>
                <ul>
                    <li><a href="https://www.bilibili.com/" style="color: var(--accent-color); text-decoration: none;">哔哩哔哩</a> - 技术视频学习</li>
                    <li><a href="https://www.anime1.me/" style="color: var(--accent-color); text-decoration: none;">Anime1</a> - 动漫观看网站</li>
                </ul>
            </div>
	</div>
</div>
<script>
        // 创建浮动图标
        function createFloatingIcons() {
            const container = document.getElementById('floatingIcons');
            const icons = ['fa-bug', 'fa-shield-alt', 'fa-code', 'fa-lock', 'fa-gamepad', 'fa-tv', 'fa-terminal', 'fa-heart', 'fa-star', 'fa-key'];
            for (let i = 0; i < 25; i++) {
                const icon = document.createElement('div');
                icon.className = 'floating-icon';
                icon.innerHTML = `<i class="fas ${icons[Math.floor(Math.random() * icons.length)]}"></i>`;
                // 随机位置
                const left = Math.random() * 100;
                const delay = Math.random() * 5;
                const duration = 10 + Math.random() * 20;
                const size = 1 + Math.random() * 2;
                icon.style.left = `${left}%`;
                icon.style.top = `${Math.random() * 100 + 100}%`;
                icon.style.animationDelay = `${delay}s`;
                icon.style.animationDuration = `${duration}s`;
                icon.style.fontSize = `${size}rem`;
                container.appendChild(icon);
            }
        }
        // 页面加载完成后执行
        window.addEventListener('load', () => {
        	createFloatingIcons();
            updateVisitorCount();
            // 为所有链接添加平滑滚动
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function(e) {
                    e.preventDefault();
                    document.querySelector(this.getAttribute('href')).scrollIntoView({
                        behavior: 'smooth'
                    });
                });
            });
        });
</script>
```

## 03 引入外部链接样式
在博客根目录的`_config.butterfly.yml`文件的`inject`的`head`中添加以下链接样式

```yaml
inject:
  head:
    - <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    - <link href="https://fonts.googleapis.com/css2?family=Ma+Shan+Zheng&family=Chewy&family=Fredoka+One&family=Caveat:wght@400;700&family=ZCOOL+KuaiLe&family=Noto+Sans+SC:wght@300;500;700&display=swap" rel="stylesheet">
```