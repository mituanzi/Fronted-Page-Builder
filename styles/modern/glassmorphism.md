# 玻璃拟态风（Glassmorphism）

> 参考：Apple macOS Big Sur、iOS 15 控制中心、Microsoft Fluent Design、Linear 部分 UI

> 适用：AI 产品、智能助手、创意工具、设计平台、高端 SaaS 产品

## 配色体系

**底色层（渐变彩底）**
```
--bg-0: #6366F1    /* 全局渐变起点，靛蓝紫 */
--bg-1: #A855F7    /* 渐变中段，紫色 */
--bg-2: #EC4899    /* 渐变终点，粉红 */
--bg-3: #F0ABFC    /* 辅助浅紫 */
```

**主色调**
```
--glass-tint: rgba(255,255,255,0.15)   /* 玻璃基底色 */
--glass-border: rgba(255,255,255,0.25) /* 玻璃边框 */
--glass-highlight: rgba(255,255,255,0.40) /* 高光边缘 */
```

**完整 :root 变量**
```css
:root {
  /* 渐变背景色 */
  --bg-0: #6366F1; --bg-1: #A855F7; --bg-2: #EC4899; --bg-3: #F0ABFC;

  /* 玻璃表面 */
  --glass-tint: rgba(255,255,255,0.15);
  --glass-tint-hover: rgba(255,255,255,0.20);
  --glass-border: rgba(255,255,255,0.25);
  --glass-highlight: rgba(255,255,255,0.40);
  --glass-dark: rgba(0,0,0,0.10);

  /* 主色 */
  --accent: #8B5CF6;          /* 紫色主交互 */
  --accent-glow: rgba(139,92,246,0.20);
  --accent-2: #EC4899;        /* 粉色辅助 */
  --accent-3: #06B6D4;        /* 青色点缀 */

  /* 语义色 */
  --success: #10B981; --warning: #F59E0B; --danger: #EF4444;

  /* 文字层级 — 玻璃面上的白色文字 */
  --text-0: #FFFFFF;     /* 标题 */
  --text-1: rgba(255,255,255,0.85);  /* 正文 */
  --text-2: rgba(255,255,255,0.65);  /* 次要 */
  --text-3: rgba(255,255,255,0.45);  /* 标签 */

  /* 边框与阴影 */
  --border: rgba(255,255,255,0.18);
  --border-strong: rgba(255,255,255,0.35);
  --shadow-sm: 0 4px 16px rgba(31,38,135,0.10);
  --shadow-md: 0 8px 32px rgba(31,38,135,0.15);
  --shadow-lg: 0 16px 48px rgba(31,38,135,0.20);

  /* 圆角 — 中大圆角 */
  --radius-sm: 10px; --radius-md: 16px; --radius-lg: 20px; --radius-xl: 24px;

  /* 缓动 */
  --ease: cubic-bezier(0.4,0,0.2,1);
  --ease-smooth: cubic-bezier(0.25,0.46,0.45,0.94);

  --header-h: 64px;
  --font-cn: "HarmonyOS Sans","Noto Sans SC","PingFang SC",sans-serif;
  --font-en: "Inter",-apple-system,sans-serif;
}
```

**设计原则**
- 背景必须是彩色渐变，玻璃效果在纯色背景上无法体现
- `backdrop-filter: blur(20px)` 是核心属性，必须配合 `-webkit-` 前缀
- 玻璃卡片需要有 1px 的半透明白色边框，模拟"玻璃边缘高光"
- 卡片内部可添加一个 `::before` 伪元素，用渐变模拟顶部高光线
- 文字必须为白色或半透明白色，确保在玻璃面上的可读性

## 背景处理

```css
body {
  background: linear-gradient(135deg, var(--bg-0) 0%, var(--bg-1) 50%, var(--bg-2) 100%);
  min-height: 100vh; color: var(--text-1);
  background-attachment: fixed;
}

/* 浮动光斑 — 增强玻璃效果可见性 */
.bg-orb {
  position: fixed; border-radius: 50%; filter: blur(80px);
  z-index: 0; pointer-events: none; opacity: 0.5;
}
.bg-orb-1 { top: -200px; left: -200px; width: 500px; height: 500px; background: var(--bg-3); }
.bg-orb-2 { bottom: -150px; right: -150px; width: 400px; height: 400px; background: var(--accent-3); opacity: 0.3; }
.bg-orb-3 {
  top: 40%; right: 10%; width: 300px; height: 300px; background: var(--accent-2); opacity: 0.25;
  animation: orbFloat 15s ease-in-out infinite;
}
@keyframes orbFloat {
  0%,100% { transform: translate(0,0); }
  50% { transform: translate(-30px, 40px); }
}
```

**HTML 结构**
```html
<div class="bg-orb bg-orb-1"></div>
<div class="bg-orb bg-orb-2"></div>
<div class="bg-orb bg-orb-3"></div>
<div id="app" style="position: relative; z-index: 1;">
  <!-- 内容 -->
</div>
```

## Header

```css
.header {
  position: fixed; top: 0; left: 0; right: 0; height: var(--header-h);
  background: var(--glass-tint); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--glass-border);
  z-index: 1000; display: flex; align-items: center; padding: 0 24px;
}
.header-title { color: var(--text-0); font-size: 18px; font-weight: 700; letter-spacing: 0.5px; }
```

## 玻璃卡片（核心组件）

```css
.glass-card {
  background: var(--glass-tint);
  backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
  border: 1px solid var(--glass-border);
  border-radius: var(--radius-lg); padding: 24px;
  box-shadow: var(--shadow-md);
  position: relative; overflow: hidden;
  transition: all 0.4s var(--ease-smooth);
}
/* 顶部高光线 */
.glass-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, transparent, var(--glass-highlight), transparent);
}
.glass-card:hover {
  background: var(--glass-tint-hover);
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}

/* 嵌套玻璃 — 卡片内的二级容器 */
.glass-inner {
  background: var(--glass-dark);
  backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
  border: 1px solid var(--border); border-radius: var(--radius-md);
  padding: 16px;
}
```

## 按钮

```css
.btn-primary {
  background: var(--accent); color: #FFFFFF;
  padding: 10px 24px; border: none; border-radius: var(--radius-md);
  font-size: 14px; font-weight: 600; cursor: pointer;
  box-shadow: 0 4px 16px var(--accent-glow);
  transition: all 0.3s var(--ease-smooth);
}
.btn-primary:hover {
  transform: translateY(-2px); box-shadow: 0 8px 24px var(--accent-glow);
}
.btn-primary:active { transform: translateY(0); }

/* 玻璃按钮 — 半透明描边 */
.btn-glass {
  background: var(--glass-tint); color: var(--text-0);
  border: 1px solid var(--glass-border);
  backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
  padding: 10px 24px; border-radius: var(--radius-md);
  font-size: 14px; font-weight: 500; cursor: pointer;
  transition: all 0.3s var(--ease-smooth);
}
.btn-glass:hover {
  background: var(--glass-tint-hover); border-color: var(--border-strong);
}
```

## 表单

```css
.input, .select, .textarea {
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
  border: 1px solid var(--border); color: var(--text-0);
  padding: 10px 14px; border-radius: var(--radius-md);
  font-size: 14px; transition: all 0.3s var(--ease-smooth);
}
.input:focus, .select:focus, .textarea:focus {
  outline: none; border-color: var(--glass-highlight);
  background: rgba(255,255,255,0.12);
  box-shadow: 0 0 0 3px rgba(255,255,255,0.10);
}
.input::placeholder { color: var(--text-3); }

/* 标签 */
.tag-glass {
  display: inline-block; padding: 4px 12px; font-size: 12px;
  background: rgba(255,255,255,0.10); border: 1px solid var(--border);
  color: var(--text-0); border-radius: var(--radius-full, 999px);
  backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px);
}
```

## Modal 样式

```css
.modal-overlay { background: rgba(30,20,60,0.40); backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px); }
.modal-box {
  background: var(--glass-tint);
  backdrop-filter: blur(40px); -webkit-backdrop-filter: blur(40px);
  border: 1px solid var(--glass-border); border-radius: var(--radius-xl);
  box-shadow: var(--shadow-lg); position: relative; overflow: hidden;
}
.modal-box::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, transparent, var(--glass-highlight), transparent);
}
.modal-head { border-bottom: 1px solid var(--border); }
.modal-foot { border-top: 1px solid var(--border); }
```

## 特色动画

```css
/* 玻璃卡片入场 — 缩放淡入 */
@keyframes glassFadeIn {
  0% { opacity: 0; transform: translateY(20px) scale(0.96); }
  100% { opacity: 1; transform: translateY(0) scale(1); }
}
.glass-in { animation: glassFadeIn 0.6s var(--ease-smooth) forwards; }

/* 悬浮光效跟随 — 鼠标位置高光 */
.glow-follow {
  position: relative; overflow: hidden;
}
.glow-follow::after {
  content: ''; position: absolute; width: 200px; height: 200px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(255,255,255,0.15), transparent 70%);
  pointer-events: none; opacity: 0; transition: opacity 0.3s;
  left: var(--mx, 50%); top: var(--my, 50%);
  transform: translate(-50%, -50%);
}
.glow-follow:hover::after { opacity: 1; }
```

```javascript
// 鼠标光效跟随
document.querySelectorAll('.glow-follow').forEach(function(el) {
  el.addEventListener('mousemove', function(e) {
    var rect = el.getBoundingClientRect();
    el.style.setProperty('--mx', (e.clientX - rect.left) + 'px');
    el.style.setProperty('--my', (e.clientY - rect.top) + 'px');
  });
});
```

## 适用场景与禁忌

- 适合：AI 产品、智能助手界面、创意工具、设计平台、高端 SaaS、产品官网
- 禁忌：不可在纯色背景上使用（必须有彩色渐变背景）；不可使用深色文字（背景已深，文字须白）；`backdrop-filter` 必须加 `-webkit-` 前缀；玻璃卡片不可堆叠超过 2 层（模糊叠加导致性能问题）；不可使用过小的圆角（<10px 会失去玻璃感的柔和感）

## 参考实现

纯 CSS+JS 实现。核心属性 `backdrop-filter: blur(Npx)`，配合彩色渐变背景和浮动光斑实现玻璃质感。

## 移动端适配

**断点规则**（在 SKILL.md 通用骨架基础上追加本风格专属规则）：

```css
/* ---- 平板 ---- */
@media (max-width: 1024px) {
  /* 渐变光晕从 3 个减为 2 个 */
  .bg-orb-3 { display: none; }
  /* backdrop-filter 降级 */
  .glass-card { backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px); }
}

/* ---- 移动端 ---- */
@media (max-width: 768px) {
  /* 仅保留 1-2 个光晕（性能 + 视觉不过载） */
  .bg-orb-2 { display: none; }
  .bg-orb-1 { width: 300px; height: 300px; opacity: 0.4; }

  /* backdrop-filter 进一步降低（低端设备关键优化） */
  .glass-card { backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); }
  .glass-heavy { backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px); }

  /* 玻璃卡片圆角从 20px 降至 16px */
  .glass-card { border-radius: 16px; }

  /* 卡片间距收紧 */
  .bento-grid { gap: 12px; }

  /* 玻璃卡片不可堆叠超过 1 层 */
  .glass-card .glass-card { backdrop-filter: none; background: rgba(255,255,255,0.06); }
}

/* ---- 小屏 ---- */
@media (max-width: 480px) {
  .glass-card { border-radius: 14px; padding: 16px; }
  .hero-title { font-size: 24px; }
}
```

**关键点**：玻璃拟态是移动端性能最敏感的风格 — `backdrop-filter` 在低端手机上帧率暴跌。必须在移动端递减 blur 值（20px → 16px → 12px → 8px），减少光晕数量，禁止嵌套玻璃层。渐变背景在移动端保留但降低光晕数量维持视觉效果。
