# Apple 极简风（Apple Minimal）

> 参考：Apple 官网、Apple 产品页、iOS 设置页、Mac App Store

> 适用：产品官网、高端品牌展示、科技公司主页、简洁工具页

## 配色体系

```css
:root {
  /* 底色层 — 纯白/极浅灰 */
  --bg-0: #FFFFFF;          /* 全局背景，纯白 */
  --bg-1: #FBFBFD;          /* 区块背景，极浅灰 */
  --bg-2: #F5F5F7;          /* 卡片/嵌套 */
  --bg-3: #E8E8ED;          /* 边缘/分隔 */

  /* 主色 — 近黑为主，蓝色为辅 */
  --accent: #1D1D1F;        /* 主色，近黑（用于文字、按钮） */
  --accent-glow: rgba(29,29,31,0.06);
  --accent-2: #0071E3;      /* 蓝色，仅用于链接和主按钮 */

  /* 语义色 */
  --success: #34C759;
  --warning: #FF9500;
  --danger: #FF3B30;

  /* 文字层级 — Apple 标准灰度阶梯 */
  --text-0: #1D1D1F;        /* 标题，近黑 */
  --text-1: #424245;        /* 正文 */
  --text-2: #6E6E73;        /* 次要 */
  --text-3: #86868B;        /* 标签/占位 */

  /* 边框 */
  --border: #D2D2D7;
  --border-strong: #86868B;

  /* 阴影 — 极轻，几乎不可见 */
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.04);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.06);
  --shadow-lg: 0 12px 40px rgba(0,0,0,0.08);

  /* 圆角 — 中等圆角 */
  --radius-sm: 8px; --radius-md: 12px; --radius-lg: 16px; --radius-xl: 20px;

  /* 缓动 — 缓慢优雅 */
  --ease: cubic-bezier(0.42,0,0.58,1);
  --ease-smooth: cubic-bezier(0.25,0.1,0.25,1);

  --header-h: 48px;
  --font-cn: "HarmonyOS Sans","Noto Sans SC","PingFang SC",sans-serif;
  --font-en: "Inter","SF Pro Display",-apple-system,sans-serif;
}
```

**设计原则**
- 留白即设计：大间距、大行高、大标题，用空间而非线条分隔内容
- 颜色极克制：全页仅黑/白/灰 + 一个蓝色点缀（`#0071E3`），禁止使用渐变背景
- 字号反差大：主标题 48-80px，正文 16-17px，通过大字号差制造视觉层次
- 阴影几乎不用：靠底色微差（`#FFFFFF` vs `#F5F5F7`）区分层级
- 所有动画时长偏长（0.6-0.8s），缓动曲线柔和

## 背景处理

```css
body { background: var(--bg-0); color: var(--text-1); }

/* 区块交替 — 白/浅灰交替 */
.section-white { background: var(--bg-0); }
.section-gray { background: var(--bg-1); }
```

不需要任何装饰性背景元素。Apple 风格的背景就是纯色。

## Header

```css
.header {
  position: fixed; top: 0; left: 0; right: 0; height: var(--header-h);
  background: rgba(255,255,255,0.72); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--border); z-index: 1000;
  display: flex; align-items: center; padding: 0 22px;
}
.header-title {
  font-size: 18px; font-weight: 600; color: var(--text-0);
  letter-spacing: -0.02em;
}
.header a { color: var(--text-0); font-size: 14px; text-decoration: none; opacity: 0.88; }
.header a:hover { opacity: 1; }
```

## 排版系统（核心）

```css
/* 超大标题 — Hero 区 */
.hero-title {
  font-size: 56px; font-weight: 700; line-height: 1.07;
  letter-spacing: -0.005em; color: var(--text-0);
  text-align: center; margin-bottom: 8px;
}
/* 大标题 */
.title-1 { font-size: 48px; font-weight: 700; line-height: 1.08; letter-spacing: -0.003em; color: var(--text-0); }
/* 中标题 */
.title-2 { font-size: 32px; font-weight: 600; line-height: 1.12; letter-spacing: 0; color: var(--text-0); }
/* 小标题 */
.title-3 { font-size: 22px; font-weight: 600; line-height: 1.2; color: var(--text-0); }
/* 正文 */
.body-text { font-size: 17px; font-weight: 400; line-height: 1.5; color: var(--text-1); }
/* 说明文字 */
.caption { font-size: 14px; font-weight: 400; line-height: 1.4; color: var(--text-2); }

/* 间距系统 */
.section { padding: 120px 22px; }
.section-tight { padding: 80px 22px; }
.content-max { max-width: 980px; margin: 0 auto; }
```

## 卡片

```css
.card {
  background: var(--bg-2); border-radius: var(--radius-lg);
  padding: 32px; transition: all 0.6s var(--ease-smooth);
}
.card:hover {
  background: var(--bg-3); transition-duration: 0.3s;
}

/* 简约白卡 — 带极轻阴影 */
.card-white {
  background: var(--bg-0); border-radius: var(--radius-lg);
  padding: 32px; box-shadow: var(--shadow-md);
  transition: all 0.6s var(--ease-smooth);
}
.card-white:hover { box-shadow: var(--shadow-lg); transform: translateY(-2px); transition-duration: 0.3s; }
```

## 按钮

```css
/* 主按钮 — 蓝色填充 */
.btn-primary {
  background: var(--accent-2); color: #FFFFFF;
  padding: 12px 28px; border: none; border-radius: var(--radius-full, 980px);
  font-size: 17px; font-weight: 400; cursor: pointer;
  transition: all 0.3s var(--ease-smooth);
}
.btn-primary:hover { background: #0077ED; }
.btn-primary:active { transform: scale(0.98); }

/* 次按钮 — 描边 */
.btn-secondary {
  background: transparent; color: var(--accent-2);
  border: 1px solid var(--accent-2);
  padding: 12px 28px; border-radius: var(--radius-full, 980px);
  font-size: 17px; font-weight: 400; cursor: pointer;
  transition: all 0.3s var(--ease-smooth);
}
.btn-secondary:hover { background: rgba(0,113,227,0.05); }

/* 文字链接按钮 — 带箭头 */
.btn-link {
  background: none; border: none; color: var(--accent-2);
  font-size: 17px; cursor: pointer; padding: 0;
  transition: all 0.2s;
}
.btn-link::after { content: ' \203A'; transition: transform 0.2s; display: inline-block; }
.btn-link:hover::after { transform: translateX(4px); }
```

## 表单

```css
.input, .select, .textarea {
  background: var(--bg-0); border: 1px solid var(--border);
  color: var(--text-0); padding: 12px 16px;
  border-radius: var(--radius-md); font-size: 17px;
  transition: all 0.3s var(--ease-smooth);
}
.input:focus, .select:focus, .textarea:focus {
  outline: none; border-color: var(--accent-2);
  box-shadow: 0 0 0 4px rgba(0,113,227,0.10);
}
.input::placeholder { color: var(--text-3); }
```

## Modal 样式

```css
.modal-overlay { background: rgba(0,0,0,0.40); backdrop-filter: blur(4px); -webkit-backdrop-filter: blur(4px); }
.modal-box {
  background: var(--bg-0); border-radius: var(--radius-xl);
  box-shadow: var(--shadow-lg);
}
.modal-head { border-bottom: 1px solid var(--border); }
.modal-foot { border-top: 1px solid var(--border); }
```

## 特色动画

```css
/* 滚动入场 — 从下方淡入 */
.reveal {
  opacity: 0; transform: translateY(40px);
  transition: opacity 0.8s var(--ease-smooth), transform 0.8s var(--ease-smooth);
}
.reveal.visible { opacity: 1; transform: translateY(0); }

/* 错峰入场 — 子元素延迟 */
.reveal:nth-child(1) { transition-delay: 0ms; }
.reveal:nth-child(2) { transition-delay: 100ms; }
.reveal:nth-child(3) { transition-delay: 200ms; }
.reveal:nth-child(4) { transition-delay: 300ms; }

/* 缩放入场 — Hero 区 */
@keyframes heroScaleIn {
  0% { opacity: 0; transform: scale(1.05); }
  100% { opacity: 1; transform: scale(1); }
}
.hero-in { animation: heroScaleIn 1.2s var(--ease-smooth) forwards; }
```

```javascript
// IntersectionObserver 滚动入场
var observer = new IntersectionObserver(function(entries) {
  entries.forEach(function(entry) {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, { threshold: 0.15 });
document.querySelectorAll('.reveal').forEach(function(el) { observer.observe(el); });
```

## 适用场景与禁忌

- 适合：产品官网、品牌展示页、科技公司主页、简洁工具介绍页、高端 SaaS 落地页
- 禁忌：不可使用彩色渐变背景；不可使用深色阴影（阴影透明度不超过 0.08）；不可使用过小的字号（正文至少 16px）；不可使用鲜艳的装饰色（蓝色是唯一允许的非灰度色）；不可使用粗糙的动画（所有 transition 时长至少 0.3s）；不可使用直角（所有圆角至少 8px）

## 移动端适配

**断点规则**（在 SKILL.md 通用骨架基础上追加本风格专属规则）：

```css
/* ---- 平板 ---- */
@media (max-width: 1024px) {
  /* 内容最大宽度收窄 */
  .content-wrapper { max-width: 720px; }
  /* 超大标题缩小 */
  .hero-title { font-size: 48px; }
}

/* ---- 移动端 ---- */
@media (max-width: 768px) {
  /* Apple 风格核心：留白保持，不压缩 */
  .section { padding: 48px 20px; }

  /* 超大标题 28px，保持层次感 */
  .hero-title { font-size: 28px; line-height: 1.15; }
  .section-title { font-size: 22px; }

  /* 胶囊按钮全宽 */
  .btn-pill { width: 100%; padding: 14px 24px; border-radius: 980px; }

  /* 产品图片全宽 */
  .product-image { width: 100%; height: auto; }

  /* 滚动动画保留但缩短 */
  .fade-up { transition: opacity 0.5s var(--ease), transform 0.5s var(--ease); }

  /* 导航简化 */
  .header-nav .nav-secondary { display: none; }
}

/* ---- 小屏 ---- */
@media (max-width: 480px) {
  .hero-title { font-size: 24px; }
  .section { padding: 40px 16px; }
  .hero-content { padding: 0; }
  /* 链接组纵向排列 */
  .link-group { flex-direction: column; gap: 12px; }
}
```

**关键点**：Apple 风格在移动端的核心原则是"留白不打折" — 即使屏幕变窄，垂直留白仍保持 48px+。标题从 64px 缩至 28px 但保持 line-height 1.15 的呼吸感。胶囊按钮全宽是 Apple 官网的移动端标准做法。滚动动画保留但缩短至 0.5s。
