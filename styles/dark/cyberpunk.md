# 未来赛博风（Cyberpunk）

> 参考：Cyberpunk 2077 UI、Tron、Blade Runner 2049、Web3 DApp
> 适用：Web3 产品、游戏平台、创意展示、未来科技概念页、AI 实验室

## 配色体系

**底色层（极深暗色）**
```
--bg-0: #0A0014   /* 全局背景，近黑带紫 */
--bg-1: #0F0020   /* 卡片背景 */
--bg-2: #1A0033   /* 悬浮/嵌套 */
--bg-3: #2A0044   /* 边缘/分隔 */
```

**主色调（荧光霓虹）**
```
--neon-cyan: #00FFFF      /* 主交互色，荧光青 */
--neon-magenta: #FF00FF   /* 辅助强调，荧光品红 */
--neon-yellow: #FFFF00    /* 警示/高亮 */
```

**语义色**
```
--success: #00FF88    /* 荧光绿 */
--warning: #FFAA00    /* 琥珀 */
--danger: #FF0044     /* 霓虹红 */
```

**文字层级**
```
--text-0: #E0FFFF   /* 标题，带青色微光 */
--text-1: #B0B0D0   /* 正文 */
--text-2: #707090   /* 次要 */
--text-3: #404060   /* 标签 */
```

**完整 :root 变量**
```css
:root {
  --bg-0: #0A0014; --bg-1: #0F0020; --bg-2: #1A0033; --bg-3: #2A0044;
  --neon-cyan: #00FFFF; --neon-magenta: #FF00FF; --neon-yellow: #FFFF00;
  --accent: var(--neon-cyan); --accent-glow: rgba(0,255,255,0.15);
  --accent-2: var(--neon-magenta);
  --success: #00FF88; --warning: #FFAA00; --danger: #FF0044;
  --text-0: #E0FFFF; --text-1: #B0B0D0; --text-2: #707090; --text-3: #404060;
  --border: rgba(0,255,255,0.15); --border-strong: rgba(0,255,255,0.40);
  --surface: rgba(15,0,32,0.85); --surface-hover: rgba(26,0,51,0.90);
  --radius-sm: 4px; --radius-md: 6px; --radius-lg: 8px; --radius-xl: 12px;
  --shadow-sm: 0 0 8px rgba(0,255,255,0.10);
  --shadow-md: 0 0 20px rgba(0,255,255,0.15), 0 0 40px rgba(255,0,255,0.08);
  --shadow-lg: 0 0 40px rgba(0,255,255,0.20), 0 0 80px rgba(255,0,255,0.10);
  --ease: cubic-bezier(0.25,0.1,0.25,1); --ease-glitch: steps(8, end);
  --header-h: 64px;
  --font-cn: "HarmonyOS Sans","Noto Sans SC","PingFang SC",sans-serif;
  --font-en: "Orbitron","Rajdhani","Inter",sans-serif;
  --font-mono: "Share Tech Mono","Courier New",monospace;
}
```

**设计原则**
- 阴影即发光：所有阴影使用荧光色 rgba 而非黑色，营造"辉光"效果
- 边框使用 `box-shadow: 0 0 Npx var(--accent)` 替代实线边框
- 文字标题可使用 `text-shadow` 添加微光，但不可过度（不超过 2px blur）
- 字体优先使用 `Orbitron`（标题）和 `Share Tech Mono`（数据），增强未来感

## 外部字体

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;500;700&family=Share+Tech+Mono&display=swap" rel="stylesheet">
```

## 背景处理

```css
body { background: var(--bg-0); color: var(--text-1); overflow-x: hidden; }

/* 赛博网格地面 — 透视网格背景 */
.bg-grid {
  position: fixed; top: 0; left: 0; width: 100%; height: 100%;
  z-index: 0; pointer-events: none;
  background-image:
    linear-gradient(rgba(0,255,255,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,255,255,0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  mask-image: linear-gradient(to bottom, transparent 0%, rgba(0,0,0,0.5) 50%, transparent 100%);
  -webkit-mask-image: linear-gradient(to bottom, transparent 0%, rgba(0,0,0,0.5) 50%, transparent 100%);
}

/* 扫描线效果 */
.bg-scanlines {
  position: fixed; top: 0; left: 0; width: 100%; height: 100%;
  z-index: 9998; pointer-events: none;
  background: repeating-linear-gradient(
    0deg, transparent 0px, transparent 2px,
    rgba(0,255,255,0.015) 2px, rgba(0,255,255,0.015) 4px
  );
}

/* 移动扫描线 */
@keyframes scanLine {
  0% { transform: translateY(-100vh); }
  100% { transform: translateY(100vh); }
}
.bg-scan-line {
  position: fixed; top: 0; left: 0; width: 100%; height: 2px; z-index: 9997;
  background: linear-gradient(90deg, transparent, var(--neon-cyan), transparent);
  opacity: 0.3; pointer-events: none;
  animation: scanLine 8s linear infinite;
}

/* 粒子 Canvas — 轻量粒子系统 */
canvas.particles { position: fixed; top: 0; left: 0; z-index: 0; pointer-events: none; }
```

**HTML 结构**
```html
<div class="bg-grid"></div>
<canvas class="particles" id="particles"></canvas>
<div class="bg-scan-line"></div>
<div class="bg-scanlines"></div>
<div id="app" style="position: relative; z-index: 1;">
  <!-- 内容 -->
</div>
```

**轻量粒子 JS**（固定 60 粒子）
```javascript
function initParticles() {
  var c = document.getElementById('particles');
  if (!c) return;
  var ctx = c.getContext('2d');
  c.width = window.innerWidth; c.height = window.innerHeight;
  var particles = [];
  for (var i = 0; i < 60; i++) {
    particles.push({
      x: Math.random() * c.width, y: Math.random() * c.height,
      vx: (Math.random() - 0.5) * 0.5, vy: (Math.random() - 0.5) * 0.5,
      r: Math.random() * 1.5 + 0.5
    });
  }
  function draw() {
    ctx.clearRect(0, 0, c.width, c.height);
    for (var i = 0; i < particles.length; i++) {
      var p = particles[i];
      p.x += p.vx; p.y += p.vy;
      if (p.x < 0 || p.x > c.width) p.vx *= -1;
      if (p.y < 0 || p.y > c.height) p.vy *= -1;
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
      ctx.fillStyle = 'rgba(0,255,255,0.4)';
      ctx.fill();
      // 连线
      for (var j = i + 1; j < particles.length; j++) {
        var q = particles[j];
        var dx = p.x - q.x, dy = p.y - q.y;
        var dist = Math.sqrt(dx * dx + dy * dy);
        if (dist < 120) {
          ctx.beginPath();
          ctx.moveTo(p.x, p.y); ctx.lineTo(q.x, q.y);
          ctx.strokeStyle = 'rgba(0,255,255,' + (0.15 * (1 - dist / 120)) + ')';
          ctx.lineWidth = 0.5;
          ctx.stroke();
        }
      }
    }
    requestAnimationFrame(draw);
  }
  draw();
  window.addEventListener('resize', function() {
    c.width = window.innerWidth; c.height = window.innerHeight;
  });
}
initParticles();
```

## Header

```css
.header {
  position: fixed; top: 0; left: 0; right: 0; height: var(--header-h);
  background: rgba(10,0,20,0.75); backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
  box-shadow: 0 1px 0 rgba(0,255,255,0.08);
  z-index: 1000; display: flex; align-items: center; padding: 0 24px;
}
.header-title {
  font-family: var(--font-en); font-size: 18px; font-weight: 900;
  color: var(--neon-cyan); text-shadow: 0 0 8px rgba(0,255,255,0.5);
  letter-spacing: 2px; text-transform: uppercase;
}
```

## 卡片

```css
.card {
  background: var(--surface); backdrop-filter: blur(8px);
  border: 1px solid var(--border); border-radius: var(--radius-md);
  padding: 20px; position: relative; overflow: hidden;
  transition: all 0.4s var(--ease);
}
.card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, transparent, var(--neon-cyan), transparent);
  opacity: 0; transition: opacity 0.4s;
}
.card:hover {
  border-color: var(--border-strong);
  box-shadow: var(--shadow-md);
  transform: translateY(-2px);
}
.card:hover::before { opacity: 1; }

/* HUD 角标 — 四角装饰 */
.card-hud::before, .card-hud::after,
.card-hud > .hud-bl, .card-hud > .hud-br {
  content: ''; position: absolute; width: 12px; height: 12px;
  border-color: var(--neon-cyan); border-style: solid; border-width: 0;
  opacity: 0.6;
}
.card-hud::before { top: 4px; left: 4px; border-top-width: 1px; border-left-width: 1px; }
.card-hud::after { top: 4px; right: 4px; border-top-width: 1px; border-right-width: 1px; }
.card-hud > .hud-bl { bottom: 4px; left: 4px; border-bottom-width: 1px; border-left-width: 1px; }
.card-hud > .hud-br { bottom: 4px; right: 4px; border-bottom-width: 1px; border-right-width: 1px; }
```

## 按钮

```css
.btn-primary {
  background: transparent; border: 1px solid var(--neon-cyan);
  color: var(--neon-cyan); padding: 10px 24px;
  font-family: var(--font-en); font-size: 14px; font-weight: 700;
  text-transform: uppercase; letter-spacing: 1px;
  border-radius: var(--radius-sm); cursor: pointer; position: relative;
  transition: all 0.3s var(--ease);
}
.btn-primary:hover {
  background: rgba(0,255,255,0.08); box-shadow: 0 0 16px rgba(0,255,255,0.30);
  text-shadow: 0 0 6px rgba(0,255,255,0.5);
}
.btn-primary:active { transform: scale(0.97); }

/* 品红渐变按钮 */
.btn-magenta {
  border-color: var(--neon-magenta); color: var(--neon-magenta);
}
.btn-magenta:hover {
  background: rgba(255,0,255,0.08); box-shadow: 0 0 16px rgba(255,0,255,0.30);
}

/* 实心荧光按钮 — 高对比 */
.btn-solid {
  background: var(--neon-cyan); color: #0A0014; border: none;
  font-weight: 900;
}
.btn-solid:hover { box-shadow: 0 0 24px rgba(0,255,255,0.50); }
```

## 表单

```css
.input, .select, .textarea {
  background: rgba(10,0,20,0.6); border: 1px solid var(--border);
  color: var(--text-0); padding: 10px 14px; border-radius: var(--radius-sm);
  font-family: var(--font-mono); font-size: 14px;
  transition: all 0.3s var(--ease);
}
.input:focus, .select:focus, .textarea:focus {
  outline: none; border-color: var(--neon-cyan);
  box-shadow: 0 0 8px rgba(0,255,255,0.20), inset 0 0 4px rgba(0,255,255,0.05);
}
.input::placeholder { color: var(--text-3); font-family: var(--font-mono); }

/* 表签 — HUD 风格标签 */
.tag-cyber {
  display: inline-block; padding: 2px 8px; font-size: 11px;
  font-family: var(--font-mono); text-transform: uppercase;
  border: 1px solid var(--border-strong); color: var(--neon-cyan);
  border-radius: var(--radius-sm); letter-spacing: 1px;
  background: rgba(0,255,255,0.05);
}
```

## Modal 样式

```css
.modal-overlay { background: rgba(5,0,10,0.80); backdrop-filter: blur(6px); }
.modal-box {
  background: linear-gradient(180deg, var(--bg-1), var(--bg-2));
  border: 1px solid var(--border-strong);
  box-shadow: 0 0 40px rgba(0,255,255,0.15), 0 0 80px rgba(255,0,255,0.08);
  border-radius: var(--radius-md); position: relative;
}
.modal-box::before {
  content: ''; position: absolute; top: -1px; left: 20px; right: 20px; height: 1px;
  background: linear-gradient(90deg, transparent, var(--neon-cyan), transparent);
}
.modal-head { border-bottom: 1px solid var(--border); }
.modal-foot { border-top: 1px solid var(--border); }
```

## 特色动画

```css
/* 故障入场 — Glitch 效果 */
@keyframes glitchIn {
  0% { opacity: 0; transform: translateX(-10px); filter: hue-rotate(90deg); }
  20% { opacity: 1; transform: translateX(10px); filter: hue-rotate(-45deg); }
  40% { transform: translateX(-4px); filter: hue-rotate(15deg); }
  60% { transform: translateX(2px); filter: hue-rotate(0deg); }
  100% { opacity: 1; transform: translateX(0); filter: hue-rotate(0deg); }
}
.glitch-in { animation: glitchIn 0.5s var(--ease-glitch) forwards; }

/* 数据流闪烁 — 用于数据值 */
@keyframes dataFlicker {
  0%,100% { opacity: 1; }
  50% { opacity: 0.85; text-shadow: 0 0 12px rgba(0,255,255,0.40); }
}
.data-value { font-family: var(--font-mono); animation: dataFlicker 3s ease-in-out infinite; }

/* HUD 边框脉冲 */
@keyframes hudPulse {
  0%,100% { box-shadow: 0 0 4px rgba(0,255,255,0.10); }
  50% { box-shadow: 0 0 16px rgba(0,255,255,0.25); }
}
.hud-pulse { animation: hudPulse 2s ease-in-out infinite; }

/* 文字霓虹闪烁 — 标题装饰 */
@keyframes neonFlicker {
  0%,100% { text-shadow: 0 0 4px rgba(0,255,255,0.5), 0 0 8px rgba(0,255,255,0.3); }
  50% { text-shadow: 0 0 6px rgba(0,255,255,0.7), 0 0 12px rgba(0,255,255,0.4); }
}
.neon-title { animation: neonFlicker 2.5s ease-in-out infinite; }
```

## 适用场景与禁忌

- 适合：Web3 产品、游戏平台、创意展示页、未来科技概念页、AI 实验室、黑客工具
- 禁忌：不可使用纯白底或浅色底；不可使用大圆角（>12px）；不可使用普通黑色阴影（必须用荧光色辉光替代）；文字不可过暗导致在深色背景上不可读；荧光色不可大面积铺色（仅用于交互元素和强调）

## 参考实现

纯CSS+JS实现，无需外部框架。粒子系统使用原生 Canvas API，60粒子固定上限保证性能。
