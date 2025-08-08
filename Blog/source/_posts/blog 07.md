---
title: butterfly主题魔改04：页面鼠标魔改-紫色水晶月光
categories: 博客搭建
tags:
  - butterfly
  - hexo
description: 实现沉浸式光标特效，包含月光主体、拖尾粒子、点击爆炸动画。通过cursor.js定义动态效果逻辑（角度追踪、悬停涟漪），custom.css添加渐变光晕与多状态图标（链接/输入框/禁用）。代码注释清晰，支持移动端自动降级。最终在_config.butterfly.yml注入资源，为博客增添独特的视觉反馈与趣味性。
top_img: /img/113.jpg
cover: /img/114.jpg
abbrlink: 9ad33db7
date: 2025-04-03 04:52:00
updated: 2025-04-03 04:52:00
swiper_index:
---
# butterfly主题魔改04：页面鼠标魔改-紫色水晶月光
## 效果图
![](https://kukual20250401-1351197034.cos.ap-guangzhou.myqcloud.com/blog/20250509160402988.gif)
## 1、创建`cursor.js`文件
在根目录`themes\butterfly\source\js`目录下创建
```js
/**
 * CrystalCursor - 水晶月光风格的自定义光标效果
 * 
 * 这个类创建了一个高度自定义的光标效果，具有以下特点：
 * 1. 月亮主题的光标主体，带有发光和脉动光环效果
 * 2. 拖尾粒子效果，跟随光标移动形成流星般的轨迹
 * 3. 点击时产生水晶爆炸和冲击波动画
 * 4. 悬停在元素上时产生涟漪效果
 * 5. 根据不同的交互元素自动改变光标样式（链接、文本输入、可拖动元素等）
 * 6. 平滑的动画和过渡效果
 * 7. 移动设备检测并禁用效果
 */

class CrystalCursor {
    constructor() {
        // 检测是否为触摸设备，如果是则不做任何处理
        if (window.matchMedia("(hover: none)").matches) {
            return;
        }

        // 初始化各种状态和属性
        this.pos = { curr: null, prev: null }; // 存储当前和之前的光标位置
        this.trailParticles = []; // 存储拖尾粒子
        this.clickParticles = []; // 存储点击粒子
        this.trailLength = 20; // 拖尾粒子的数量
        this.lastEmitTime = 0; // 上次发射粒子的时间
        this.angle = 0; // 光标移动角度
        this.currentPointer = 'normal'; // 当前指针类型
        // 线性插值函数，用于平滑移动
        this.lerp = (a, b, n) => (1 - n) * a + n * b;
        
        // 创建光标DOM元素
        this.cursor = document.createElement("div");
        this.cursor.id = "moonlight-cursor";
        this.cursor.className = "hidden"; // 初始隐藏
        // 光标内部结构：月亮圆盘、月牙、发光效果和三个光环
        this.cursor.innerHTML = `
            <div class="moon-disc"></div>
            <div class="moon-crescent"></div>
            <div class="moon-glow"></div>
            <div class="moon-rings">
                <div class="ring ring-1"></div>
                <div class="ring ring-2"></div>
                <div class="ring ring-3"></div>
            </div>
        `;
        document.body.append(this.cursor);
        
        // 创建拖尾粒子
        for (let i = 0; i < this.trailLength; i++) {
            const particle = document.createElement("div");
            particle.className = "crystal-trail";
            particle.style.setProperty('--i', i);
            document.body.appendChild(particle);
            // 每个粒子有自己的位置、大小、延迟等属性
            this.trailParticles.push({
                el: particle,
                pos: { x: 0, y: 0 },
                size: 1 + Math.random() * 1.5,
                delay: i * 0.02,
                life: 0,
                speed: 0.5 + Math.random() * 0.5,
                angle: 0
            });
        }
        
        // 初始化事件监听器
        this.initEventListeners();
        // 开始渲染动画
        this.raf = requestAnimationFrame(() => this.render());
    }

    // 初始化所有事件监听器
    initEventListeners() {
        // 绑定各种事件处理方法
        this.mouseMoveHandler = e => this.handleMouseMove(e);
        this.mouseEnterHandler = () => this.cursor.classList.remove("hidden");
        this.mouseLeaveHandler = () => this.cursor.classList.add("hidden");
        this.mouseDownHandler = e => this.handleMouseDown(e);
        this.mouseUpHandler = () => this.cursor.classList.remove("active");
        
        // 添加基本鼠标事件监听
        document.addEventListener('mousemove', this.mouseMoveHandler);
        document.addEventListener('mouseenter', this.mouseEnterHandler);
        document.addEventListener('mouseleave', this.mouseLeaveHandler);
        document.addEventListener('mousedown', this.mouseDownHandler);
        document.addEventListener('mouseup', this.mouseUpHandler);
        
        // 为可悬停元素添加事件监听
        this.hoverElements = document.querySelectorAll('a, button, [data-hover]');
        this.hoverElements.forEach(el => {
            el.addEventListener('mouseenter', this.handleHoverEnter.bind(this));
            el.addEventListener('mouseleave', this.handleHoverLeave.bind(this));
        });

        // 为文本输入元素添加事件监听
        this.textElements = document.querySelectorAll('input, textarea, [contenteditable]');
        this.textElements.forEach(el => {
            el.addEventListener('mouseenter', () => this.setPointer('text'));
            el.addEventListener('mouseleave', () => this.setPointer('normal'));
        });

        // 为禁用元素添加事件监听
        this.disabledElements = document.querySelectorAll('[disabled]');
        this.disabledElements.forEach(el => {
            el.addEventListener('mouseenter', () => this.setPointer('unavailable'));
            el.addEventListener('mouseleave', () => this.setPointer('normal'));
        });

        // 为可拖动元素添加事件监听
        this.draggableElements = document.querySelectorAll('[draggable="true"]');
        this.draggableElements.forEach(el => {
            el.addEventListener('mouseenter', () => this.setPointer('move'));
            el.addEventListener('mouseleave', () => this.setPointer('normal'));
        });
    }

    // 处理鼠标移动事件
    handleMouseMove(e) {
        const now = Date.now();
        // 限制粒子发射频率
        if (now - this.lastEmitTime > 16) {
            // 如果是第一次移动，初始化位置
            if (this.pos.curr === null) {
                this.move(e.clientX - 6, e.clientY - 6);
            }
            // 更新当前位置
            this.pos.curr = { x: e.clientX, y: e.clientY };
            this.cursor.classList.remove("hidden");
            
            // 计算移动角度
            if (this.pos.prev) {
                const dx = this.pos.curr.x - this.pos.prev.x;
                const dy = this.pos.curr.y - this.pos.prev.y;
                this.angle = Math.atan2(dy, dx);
            }
            
            // 激活拖尾粒子
            this.activateTrailParticle();
            this.lastEmitTime = now;
        }
    }

    // 处理鼠标按下事件
    handleMouseDown(e) {
        this.cursor.classList.add("active");
        const scrollX = window.scrollX || window.pageXOffset;
        const scrollY = window.scrollY || window.pageYOffset;
        // 创建点击效果
        this.createCrystalBurst(e.clientX + scrollX, e.clientY + scrollY);
        this.createShockwave(e.clientX + scrollX, e.clientY + scrollY);
    }

    // 处理悬停进入事件
    handleHoverEnter(e) {
        this.setPointer('link');
        this.cursor.classList.add('hover');
        const rect = e.target.getBoundingClientRect();
        // 创建涟漪效果
        this.createRippleEffect(rect);
    }

    // 处理悬停离开事件
    handleHoverLeave() {
        this.setPointer('normal');
        this.cursor.classList.remove('hover');
    }

    // 设置指针样式
    setPointer(type) {
        this.currentPointer = type;
        // 定义不同类型的光标样式映射
        const cursorMap = {
            normal: 'url(/img/normal.cur), default',
            link: 'url(/img/link.cur), pointer',
            text: 'url(/img/text.cur), text',
            move: 'url(/img/move.cur), move',
            help: 'url(/img/help.cur), help',
            unavailable: 'url(/img/unavailable.cur), not-allowed',
            busy: 'url(/img/busy.ani), wait',
            working: 'url(/img/working.ani), progress',
            precision: 'url(/img/precision.cur), crosshair'
        };

        document.body.style.cursor = cursorMap[type] || cursorMap.normal;
    }

    // 移动光标到指定位置
    move(left, top) {
        this.cursor.style.left = `${left}px`;
        this.cursor.style.top = `${top}px`;
    }

    // 激活拖尾粒子
    activateTrailParticle() {
        // 找到一个可用的粒子
        const particle = this.trailParticles.find(p => p.life <= 0);
        if (particle && this.pos.prev) {
            // 初始化粒子属性
            particle.life = 1;
            particle.pos.x = this.pos.prev.x;
            particle.pos.y = this.pos.prev.y;
            particle.size = 1 + Math.random() * 2;
            particle.el.style.width = `${particle.size}px`;
            particle.el.style.height = `${particle.size * 1.5}px`;
            particle.el.style.opacity = '0.8';
            particle.el.style.borderRadius = '50%';
            
            // 设置粒子角度
            if (this.angle) {
                particle.angle = this.angle;
                particle.el.style.transform = `translate(-50%, -50%) rotate(${particle.angle + Math.PI/2}rad)`;
            }
            
            // 设置粒子颜色和发光效果
            const hue = 270 + Math.random() * 30 - 15;
            particle.el.style.background = `linear-gradient(to bottom, 
                hsla(${hue}, 100%, 70%, 0.9), 
                hsla(${hue + 20}, 100%, 50%, 0.5))`;
            particle.el.style.boxShadow = `0 0 5px hsla(${hue}, 100%, 70%, 0.8)`;
        }
    }

    // 创建水晶爆炸效果
    createCrystalBurst(x, y) {
        const colors = ['#8a2be2', '#9932cc', '#ba55d3', '#da70d6', '#d8bfd8'];
        const count = 50; // 爆炸粒子数量
        
        for (let i = 0; i < count; i++) {
            const crystal = document.createElement('div');
            crystal.className = 'crystal-burst';
            crystal.style.left = `${x}px`;
            crystal.style.top = `${y}px`;
            crystal.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
            document.body.appendChild(crystal);
            
            // 设置粒子动画属性
            const angle = Math.random() * Math.PI * 2;
            const velocity = 0.5 + Math.random() * 2;
            const lifetime = 800 + Math.random() * 400;
            const size = 2 + Math.random() * 12;
            const rotation = Math.random() * 360;
            
            crystal.style.width = `${size}px`;
            crystal.style.height = `${size}px`;
            crystal.style.transform = `rotate(${rotation}deg)`;
            crystal.style.clipPath = 'polygon(50% 0%, 0% 100%, 100% 100%)';
            
            // 粒子动画函数
            const animate = (startTime) => {
                const now = Date.now();
                const progress = (now - startTime) / lifetime;
                
                if (progress >= 1) {
                    crystal.remove();
                    return;
                }
                
                // 计算粒子当前位置和状态
                const distance = velocity * progress * 50;
                const currentX = x + Math.cos(angle) * distance;
                const currentY = y + Math.sin(angle) * distance;
                const opacity = 1 - progress;
                const scale = 0.5 + progress * 0.5;
                
                // 更新粒子样式
                crystal.style.transform = `translate(${currentX - x}px, ${currentY - y}px) rotate(${rotation + progress * 360}deg) scale(${scale})`;
                crystal.style.opacity = opacity;
                
                requestAnimationFrame(() => animate(startTime));
            };
            
            requestAnimationFrame(() => animate(Date.now()));
        }
    }

    // 创建冲击波效果
    createShockwave(x, y) {
        const wave = document.createElement('div');
        wave.className = 'shockwave';
        wave.style.left = `${x}px`;
        wave.style.top = `${y}px`;
        document.body.appendChild(wave);
        
        const startTime = Date.now();
        const duration = 600;
        
        // 冲击波动画函数
        const animate = () => {
            const now = Date.now();
            const progress = (now - startTime) / duration;
            
            if (progress >= 1) {
                wave.remove();
                return;
            }
            
            // 计算冲击波大小和透明度
            const size = progress * 50;
            const opacity = 1 - progress;
            
            wave.style.width = `${size}px`;
            wave.style.height = `${size}px`;
            wave.style.opacity = opacity;
            wave.style.borderWidth = `${1 - progress * 1}px`;
            
            requestAnimationFrame(animate);
        };
        
        requestAnimationFrame(animate);
    }

    // 创建悬停时的涟漪效果
    createRippleEffect(rect) {
        const scrollX = window.scrollX || window.pageXOffset;
        const scrollY = window.scrollY || window.pageYOffset;
        const ripple = document.createElement('div');
        ripple.className = 'ripple-effect';
        ripple.style.left = `${rect.left + rect.width/2 + scrollX}px`;
        ripple.style.top = `${rect.top + rect.height/2 + scrollY}px`;
        document.body.appendChild(ripple);
        
        // 1秒后移除涟漪元素
        setTimeout(() => {
            ripple.remove();
        }, 1000);
    }

    // 主渲染函数
    render() {
        if (this.pos.prev && this.pos.curr) {
            // 使用线性插值平滑移动光标
            this.pos.prev.x = this.lerp(this.pos.prev.x, this.pos.curr.x, 0.2);
            this.pos.prev.y = this.lerp(this.pos.prev.y, this.pos.curr.y, 0.2);
            this.move(this.pos.prev.x - 6, this.pos.prev.y - 6);
            
            // 更新拖尾粒子
            this.trailParticles.forEach((p) => {
                if (p.life > 0) {
                    p.life -= p.speed * 0.02;
                    
                    // 根据角度移动粒子
                    const distance = (1 - p.life) * 15;
                    p.pos.x += Math.cos(p.angle) * distance * 0.1;
                    p.pos.y += Math.sin(p.angle) * distance * 0.1;
                    
                    // 更新粒子位置和透明度
                    p.el.style.left = `${p.pos.x}px`;
                    p.el.style.top = `${p.pos.y}px`;
                    p.el.style.opacity = p.life * 0.8;
                    
                    // 粒子拖尾长度变化
                    const tailLength = 3 + (1 - p.life) * 2.5;
                    p.el.style.height = `${p.size * tailLength}px`;
                    
                    if (p.life <= 0) {
                        p.el.style.opacity = '0';
                    }
                }
            });
            
            // 月亮发光强度变化
            const glowIntensity = Math.abs(Math.sin(Date.now() * 0.003)) * 0.3 + 0.7;
            this.cursor.querySelector('.moon-glow').style.opacity = glowIntensity;
            
            // 光环脉动效果
            const pulse = Math.abs(Math.sin(Date.now() * 0.002)) * 0.2 + 0.8;
            this.cursor.querySelector('.ring-1').style.transform = `translate(-50%, -50%) scale(${pulse})`;
            this.cursor.querySelector('.ring-2').style.transform = `translate(-50%, -50%) scale(${pulse * 1.1})`;
            this.cursor.querySelector('.ring-3').style.transform = `translate(-50%, -50%) scale(${pulse * 1.2})`;
        } else {
            this.pos.prev = this.pos.curr;
        }
        
        // 继续渲染循环
        this.raf = requestAnimationFrame(() => this.render());
    }

    // 销毁方法，清理所有资源和事件监听
    destroy() {
        cancelAnimationFrame(this.raf);
        
        // 移除所有事件监听
        document.removeEventListener('mousemove', this.mouseMoveHandler);
        document.removeEventListener('mouseenter', this.mouseEnterHandler);
        document.removeEventListener('mouseleave', this.mouseLeaveHandler);
        document.removeEventListener('mousedown', this.mouseDownHandler);
        document.removeEventListener('mouseup', this.mouseUpHandler);
        
        this.hoverElements.forEach(el => {
            el.removeEventListener('mouseenter', this.handleHoverEnter);
            el.removeEventListener('mouseleave', this.handleHoverLeave);
        });
        
        this.textElements.forEach(el => {
            el.removeEventListener('mouseenter', () => this.setPointer('text'));
            el.removeEventListener('mouseleave', () => this.setPointer('normal'));
        });
        
        this.disabledElements.forEach(el => {
            el.removeEventListener('mouseenter', () => this.setPointer('unavailable'));
            el.removeEventListener('mouseleave', () => this.setPointer('normal'));
        });
        
        this.draggableElements.forEach(el => {
            el.removeEventListener('mouseenter', () => this.setPointer('move'));
            el.removeEventListener('mouseleave', () => this.setPointer('normal'));
        });
        
        // 移除所有DOM元素
        this.cursor.remove();
        this.trailParticles.forEach(p => p.el.remove());
        document.body.style.cursor = '';
    }
}

// 立即执行函数，创建并管理光标实例
(() => {
    const CRYSTAL_CURSOR = new CrystalCursor();
    // 页面卸载前清理资源
    window.addEventListener('beforeunload', () => {
        CRYSTAL_CURSOR.destroy();
    });
})();
```
## 2、创建`custom.css`文件
在根目录`themes\butterfly\source\css`目录下创建
```css
/* 
 * Moonlight Cursor 月光光标效果
 * 
 * 这是一个自定义的光标系统，用CSS和少量JavaScript（未包含在此）实现
 * 主要功能：
 * 1. 替换默认光标为月光主题的圆形光标
 * 2. 悬停在不同元素上时有不同的视觉效果
 * 3. 包含光晕、月牙、光环等装饰元素
 * 4. 支持点击动画和拖尾效果
 * 5. 为不同交互状态提供不同的光标图标
 * 6. 响应式设计，在触摸设备上自动隐藏
 */

/* 主光标容器 - 固定在视口中，跟随鼠标移动 */
#moonlight-cursor {
  position: fixed;       /* 固定定位，不随页面滚动 */
  width: 16px;           /* 基础宽度 */
  height: 16px;          /* 基础高度 */
  pointer-events: none;  /* 防止光标元素拦截鼠标事件 */
  z-index: 9999;         /* 确保显示在最顶层 */
  transform: translate(-50%, -50%); /* 居中定位 */
  transition: transform 0.1s ease;  /* 移动时的平滑过渡 */
}

/* 隐藏状态的光标 */
#moonlight-cursor.hidden {
  opacity: 0;                   /* 完全透明 */
  transition: opacity 0.3s ease; /* 淡出过渡效果 */
}

/* 月亮圆盘 - 光标的基础圆形部分 */
.moon-disc {
  position: absolute;      /* 绝对定位 */
  width: 100%;            /* 充满容器 */
  height: 100%;           /* 充满容器 */
  background: rgba(117, 49, 177, 0.2); /* 半透明紫色背景 */
  border-radius: 50%;      /* 圆形 */
  box-shadow: 0 0 8px #6624a0,  /* 外发光效果 */
              inset 0 0 5px #6420a0; /* 内发光效果 */
  transition: all 0.3s ease; /* 所有属性的过渡效果 */
}

/* 月牙形状 - 月亮上的凹陷部分 */
.moon-crescent {
  position: absolute;      /* 绝对定位 */
  width: 60%;             /* 相对宽度 */
  height: 60%;            /* 相对高度 */
  left: 10%;              /* 水平位置 */
  top: 20%;               /* 垂直位置 */
  background: transparent; /* 透明背景 */
  border-radius: 50%;     /* 圆形 */
  box-shadow: inset 3px -3px 0 0 #c08bdf; /* 内阴影创建月牙效果 */
  transform: rotate(45deg); /* 旋转45度 */
  transition: all 0.3s ease; /* 所有属性的过渡效果 */
}

/* 光晕效果 - 围绕月亮的发光效果 */
.moon-glow {
  position: absolute;      /* 绝对定位 */
  width: 140%;            /* 比容器大 */
  height: 140%;           /* 比容器大 */
  left: -20%;             /* 居中定位 */
  top: -20%;              /* 居中定位 */
  background: radial-gradient(circle,  /* 径向渐变 */
              rgba(224, 170, 255, 0.3) 0%,  /* 中心颜色 */
              transparent 60%);        /* 边缘透明 */
  border-radius: 50%;     /* 圆形 */
  opacity: 0.7;           /* 半透明 */
  transition: opacity 0.5s ease; /* 透明度过渡效果 */
}

/* 光环容器 */
.moon-rings {
  position: absolute;      /* 绝对定位 */
  width: 100%;            /* 充满容器 */
  height: 100%;           /* 充满容器 */
}

/* 单个光环 */
.ring {
  position: absolute;      /* 绝对定位 */
  border-radius: 50%;     /* 圆形 */
  border-style: solid;    /* 实线边框 */
  border-color: #9b59b6;  /* 紫色边框 */
  transform: translate(-50%, -50%); /* 居中定位 */
  transition: all 0.3s ease-out; /* 所有属性的过渡效果 */
}

/* 第一层光环 */
.ring-1 {
  width: 120%;            /* 比容器大 */
  height: 120%;          /* 比容器大 */
  top: 50%;              /* 垂直居中 */
  left: 50%;             /* 水平居中 */
  border-width: 1px;     /* 边框宽度 */
  opacity: 0.5;          /* 半透明 */
}

/* 第二层光环 */
.ring-2 {
  width: 150%;           /* 比第一层大 */
  height: 150%;         /* 比第一层大 */
  top: 50%;             /* 垂直居中 */
  left: 50%;            /* 水平居中 */
  border-width: 1px;    /* 边框宽度 */
  opacity: 0.3;         /* 更透明 */
}

/* 第三层光环 */
.ring-3 {
  width: 180%;          /* 最大的光环 */
  height: 180%;        /* 最大的光环 */
  top: 50%;           /* 垂直居中 */
  left: 50%;          /* 水平居中 */
  border-width: 1px;  /* 边框宽度 */
  opacity: 0.2;       /* 最透明 */
}

/* 悬停状态下的光标样式 */
#moonlight-cursor.hover .moon-disc {
  background: rgba(157, 78, 221, 0.3); /* 更亮的背景 */
  box-shadow: 0 0 10px #9d4edd,  /* 更强的外发光 */
              inset 0 0 8px #9d4edd; /* 更强的内发光 */
}

#moonlight-cursor.hover .moon-crescent {
  box-shadow: inset 3px -3px 0 0 #c77dff; /* 更亮的月牙 */
}

/* 悬停时光环的动画效果 */
#moonlight-cursor.hover .ring-1 {
  opacity: 0.8;          /* 更明显 */
  transform: translate(-50%, -50%) scale(1.1); /* 轻微放大 */
}

#moonlight-cursor.hover .ring-2 {
  opacity: 0.6;          /* 更明显 */
  transform: translate(-50%, -50%) scale(1.1); /* 轻微放大 */
}

#moonlight-cursor.hover .ring-3 {
  opacity: 0.4;          /* 更明显 */
  transform: translate(-50%, -50%) scale(1.1); /* 轻微放大 */
}

/* 点击激活状态 */
#moonlight-cursor.active {
  transform: translate(-50%, -50%) scale(0.8); /* 点击时缩小 */
}

/* 水晶拖尾效果 */
.crystal-trail {
  position: fixed;       /* 固定定位 */
  pointer-events: none;  /* 不拦截鼠标事件 */
  z-index: 9998;        /* 仅次于主光标 */
  opacity: 0;           /* 默认透明 */
  transition: opacity 0.2s ease; /* 淡入淡出效果 */
  transform-origin: center; /* 变换中心点 */
  background: linear-gradient(to bottom, #e0aaff, #9d4edd); /* 渐变背景 */
  box-shadow: 0 0 5px rgba(157, 78, 221, 0.8); /* 发光效果 */
}

/* 水晶爆发效果 */
.crystal-burst {
  position: absolute;    /* 绝对定位 */
  pointer-events: none;  /* 不拦截鼠标事件 */
  z-index: 9997;        /* 层级 */
  transform-origin: center; /* 变换中心点 */
  opacity: 0.8;         /* 半透明 */
  filter: drop-shadow(0 0 3px currentColor); /* 发光效果 */
}

/* 冲击波动画 */
.shockwave {
  position: absolute;    /* 绝对定位 */
  border-radius: 50%;   /* 圆形 */
  border: 1px solid #9d4edd; /* 紫色边框 */
  transform: translate(-50%, -50%); /* 居中 */
  pointer-events: none; /* 不拦截鼠标事件 */
  z-index: 9996;       /* 层级 */
  opacity: 0.8;        /* 半透明 */
  transition: all 0.3s ease-out; /* 过渡效果 */
}

/* 涟漪效果 */
.ripple-effect {
  position: absolute;    /* 绝对定位 */
  width: 0;             /* 初始大小 */
  height: 0;            /* 初始大小 */
  border-radius: 50%;   /* 圆形 */
  background: rgba(157, 78, 221, 0.2); /* 半透明紫色 */
  transform: translate(-50%, -50%); /* 居中 */
  pointer-events: none; /* 不拦截鼠标事件 */
  z-index: 9995;       /* 层级 */
  animation: ripple 0.8s ease-out forwards; /* 涟漪动画 */
}

/* 涟漪动画关键帧 */
@keyframes ripple {
  to {
    width: 100px;       /* 放大到100px */
    height: 100px;      /* 放大到100px */
    opacity: 0;         /* 淡出 */
  }
}

/* 水晶脉动动画关键帧 */
@keyframes crystal-pulse {
  0% { transform: scale(0.9); opacity: 0.8; } /* 初始状态 */
  50% { transform: scale(1.1); opacity: 1; }  /* 放大变亮 */
  100% { transform: scale(0.9); opacity: 0.8; } /* 恢复 */
}

/* 默认光标替换 */
html {
  cursor: url('/img/normal.cur'), default !important; /* 自定义光标，回退到默认 */
}

/* 链接状态光标 */
a, [href], [data-hover] {
  cursor: url('/img/link.cur'), pointer !important; /* 链接光标 */
}

/* 文本输入状态光标 */
input, textarea, [contenteditable] {
  cursor: url('/img/text.cur'), text !important; /* 文本光标 */
}

/* 可拖动元素光标 */
[draggable="true"] {
  cursor: url('/img/move.cur'), move !important; /* 移动光标 */
}

/* 禁用状态光标 */
[disabled] {
  cursor: url('/img/unavailable.cur'), not-allowed !important; /* 禁用光标 */
}

/* 忙碌状态光标 */
.busy-cursor {
  cursor: url('/img/busy.ani'), wait !important; /* 等待光标(动画) */
}

/* 精确选择光标 */
.precision-cursor {
  cursor: url('/img/precision.cur'), crosshair !important; /* 十字光标 */
}

/* 帮助状态光标 */
.help-cursor {
  cursor: url('/img/help.cur'), help !important; /* 帮助光标 */
}

/* 触摸设备适配 - 隐藏自定义光标 */
@media (hover: none) {
  #moonlight-cursor, .crystal-trail {
      display: none !important; /* 触摸设备上隐藏 */
  }
  
  body {
      cursor: default !important; /* 使用系统默认光标 */
  }
}
```
## 3、修改`_config.butterfly.yml`
根目录下`_config.butterfly.yml`文件，修改`inject`部分，引入样式地址。
```yaml
inject:
  head:
    - <link rel="stylesheet" href="/css/custom.css"> 
  bottom:
    - <script defer src="/js/cursor.js"></script> 

```
