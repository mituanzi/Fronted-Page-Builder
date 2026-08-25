# 国风雅致风（Chinese Elegant）

> 参考：故宫文创、中国传统文化展示、茶道/书画展示

> 适用：文化展示、博物馆数字馆、传统工艺平台、茶文化/书画展示

## 配色体系

```css
:root {
  /* 底色层 — 宣纸/米色基底 */
  --bg-0: #F5F0E8;          /* 宣纸白 */
  --bg-1: #FAF6EF;          /* 卡片浅米 */
  --bg-2: #EDE6D8;          /* 悬浮深米 */
  --bg-3: #DDD3C0;          /* 边缘 */

  /* 主色调 — 传统中国色 */
  --accent: #8B2C2C;         /* 朱砂红 */
  --accent-glow: rgba(139,44,44,0.08);
  --accent-2: #2C5F7C;       /* 青黛蓝 */
  --accent-3: #5B7A3A;       /* 苍翠绿 */
  --accent-4: #8B6914;       /* 赭石金 */

  /* 语义色 */
  --success: #5B7A3A;
  --warning: #8B6914;
  --danger: #8B2C2C;

  /* 文字层级 — 水墨灰 */
  --text-0: #2C2420;        /* 浓墨 */
  --text-1: #4A3F38;        /* 淡墨 */
  --text-2: #7A6E64;        /* 灰墨 */
  --text-3: #A89A8C;        /* 浅墨 */

  /* 边框与表面 */
  --border: #DDD3C0;
  --border-strong: #C4B8A0;
  --surface: rgba(250,246,239,0.85);
  --surface-hover: rgba(237,230,216,0.90);

  /* 圆角 — 适中，温润 */
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 14px;
  --radius-xl: 20px;

  /* 阴影 — 轻柔，暖色调 */
  --shadow-sm: 0 2px 8px rgba(74,63,56,0.04);
  --shadow-md: 0 6px 20px rgba(74,63,56,0.06);
  --shadow-lg: 0 12px 40px rgba(74,63,56,0.10);

  /* 缓动 — 缓慢柔和 */
  --ease: cubic-bezier(0.4,0,0.2,1);
  --ease-bounce: cubic-bezier(0.34,1.56,0.64,1);

  /* 字体 — 衬线为主 */
  --font-cn: "Noto Serif SC","Source Han Serif SC","STSong","SimSun",serif;
  --font-en: "Cormorant Garamond","Georgia",serif;
  --font-sans: "Noto Sans SC","PingFang SC",sans-serif;
}
```

## 背景处理

```css
body { background: var(--bg-0); color: var(--text-1); font-family: var(--font-cn); }
/* 水墨纹理 */
.bg-ink {
  position: fixed; top: 0; left: 0; right: 0; height: 500px; z-index: 0; pointer-events: none;
  background: radial-gradient(ellipse 60% 40% at 50% 0%, rgba(44,95,124,0.04), transparent 70%);
}
/* 可选：纸纹叠加 */
.bg-paper {
  position: fixed; inset: 0; z-index: 0; pointer-events: none; opacity: 0.4;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='4'/%3E%3CfeColorMatrix values='0 0 0 0 0.5 0 0 0 0 0.4 0 0 0 0 0.3 0 0 0 0.03 0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}
```

## Header

```css
.header {
  position: fixed; top: 0; left: 0; right: 0; height: 64px; z-index: 1000;
  background: rgba(245,240,232,0.92);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
}
.header-left .h-title { font-family: var(--font-cn); letter-spacing: 4px; font-weight: 600; }
.header-left .h-sub { font-family: var(--font-en); letter-spacing: 2px; font-style: italic; }
```

## 卡片

```css
.card {
  background: var(--bg-1);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 28px;
  box-shadow: var(--shadow-sm);
  transition: all 0.4s var(--ease);
}
.card:hover {
  border-color: var(--border-strong);
  box-shadow: var(--shadow-md);
}
```

## 按钮

```css
.btn-primary {
  background: var(--accent);
  color: var(--bg-1);
  border-radius: var(--radius-sm);
  font-family: var(--font-cn);
  letter-spacing: 2px;
}
.btn-primary:hover { background: #6B1F1F; }
.btn-ghost {
  border: 1px solid var(--border-strong);
  color: var(--text-1);
  background: var(--bg-1);
  border-radius: var(--radius-sm);
}
.btn-ghost:hover { border-color: var(--accent); color: var(--accent); }
```

## 表单

```css
.form-input {
  background: var(--bg-1);
  border: 1px solid var(--border);
  color: var(--text-0);
  border-radius: var(--radius-sm);
  font-family: var(--font-sans); /* 输入框用无衬线保证可读性 */
}
.form-input:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px var(--accent-glow);
}
```

## Modal

```css
.modal-overlay { background: rgba(44,36,32,0.45); backdrop-filter: blur(6px); }
.modal-box {
  background: var(--bg-1);
  border: 1px solid var(--border-strong);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
}
.modal-head .m-title { font-family: var(--font-cn); letter-spacing: 3px; }
```

## 特色元素

**分隔线 — 中式纹样**
```css
.divider-cn {
  text-align: center; margin: 32px 0; position: relative;
}
.divider-cn::before, .divider-cn::after {
  content: ''; position: absolute; top: 50%; width: 40%; height: 1px;
  background: linear-gradient(90deg, transparent, var(--border-strong), transparent);
}
.divider-cn::before { left: 0; }
.divider-cn::after { right: 0; }
.divider-cn span { background: var(--bg-0); padding: 0 16px; color: var(--text-3); font-family: var(--font-cn); }
```

**标签 — 印章风格**
```css
.seal {
  display: inline-flex; align-items: center; justify-content: center;
  width: 48px; height: 48px;
  background: var(--accent); color: var(--bg-1);
  border-radius: 4px; font-family: var(--font-cn); font-size: 14px; font-weight: 600;
  letter-spacing: 2px; line-height: 1.2; text-align: center;
  box-shadow: 0 2px 8px rgba(139,44,44,0.15);
}
```

**标题装饰 — 竖线**
```css
.section-title-cn {
  font-family: var(--font-cn); font-size: 24px; font-weight: 600;
  letter-spacing: 4px; color: var(--text-0);
  padding-left: 16px; border-left: 3px solid var(--accent);
}
```

## 动画

```css
/* 缓慢淡入 */
.fade-up { opacity: 0; transform: translateY(20px); transition: opacity 1s var(--ease), transform 1s var(--ease); }
.fade-up.visible { opacity: 1; transform: translateY(0); }
/* 不使用 bounce，保持优雅 */
```

## 排版规范

- 中文标题使用衬线体（Noto Serif SC），字号略大，letter-spacing 3-5px
- 英文标题使用 Cormorant Garamond 斜体
- 正文可使用无衬线体保证可读性（Noto Sans SC）
- 大量留白：段间距 24-32px，区块间距 100-120px
- 行高：标题 1.4，正文 1.8（宽松）

## 适用场景与禁忌

- 适合：文化展示、博物馆数字馆、传统工艺、茶文化、书画展示、国潮品牌
- 禁忌：不可使用荧光色/纯白底；不可使用方圆角过大；不可使用 emoji；正文字号不可小于 14px

## 移动端适配

**断点规则**（在 SKILL.md 通用骨架基础上追加本风格专属规则）：

```css
/* ---- 平板 ---- */
@media (max-width: 1024px) {
  .content-wrapper { max-width: 720px; }
  .gallery-grid { grid-template-columns: repeat(2, 1fr); }
}

/* ---- 移动端 ---- */
@media (max-width: 768px) {
  /* 水墨装饰元素隐藏（性能 + 小屏视觉过载） */
  .ink-decoration, .ink-splash { display: none; }

  /* 留白保持（国风核心特征） */
  .section { padding: 48px 20px; }

  /* 衬线字体最小 16px（可读性） */
  .body-text { font-size: 16px; line-height: 1.8; }

  /* 印章装饰缩小 */
  .seal { width: 48px; height: 48px; }

  /* 标题保持层次 */
  .hero-title { font-size: 28px; }
  .section-title { font-size: 22px; }

  /* 画廊单列 */
  .gallery-grid { grid-template-columns: 1fr; }

  /* 宣纸纹理保留但降低透明度 */
  .paper-texture { opacity: 0.3; }
}

/* ---- 小屏 ---- */
@media (max-width: 480px) {
  .hero-title { font-size: 24px; }
  .section { padding: 36px 16px; }
  .seal { width: 36px; height: 36px; }
  .body-text { font-size: 15px; }
  /* 垂直书写降级为水平（小屏无法支撑竖排） */
  .vertical-text { writing-mode: horizontal-tb; }
}
```

**关键点**：国风雅致在移动端的核心是"留白不打折"和"衬线可读性"。水墨装饰在移动端隐藏（GPU 性能 + 小屏视觉过载），但宣纸纹理保留（降低透明度）。竖排文字在小屏降级为横排（`writing-mode: horizontal-tb`），因为窄屏无法支撑竖排的阅读体验。正文字号最小 15px 保证衬线字体的可读性。
