# 明亮科技风（Bright Tech）

> 参考：Apple、Notion、Stripe、Linear Docs

> 适用：SaaS 产品、管理后台、文档平台、数据工具

## 配色体系

```css
:root {
  /* 底色层 */
  --bg-0: #FFFFFF;          /* 全局背景 */
  --bg-1: #F7F9FC;          /* 卡片/区块背景 */
  --bg-2: #EEF2F7;          /* 嵌套/悬浮背景 */
  --bg-3: #E2E8F0;          /* 边缘/分隔 */

  /* 主色调 */
  --accent: #0066FF;         /* 主交互蓝 */
  --accent-glow: rgba(0,102,255,0.10); /* 主色光晕 */
  --accent-2: #6B46FF;       /* 辅助紫 */

  /* 语义色 */
  --success: #00B884;
  --warning: #FF8800;
  --danger: #E53E3E;

  /* 文字层级 */
  --text-0: #1A202C;        /* 标题 */
  --text-1: #2D3748;        /* 正文 */
  --text-2: #718096;        /* 次要 */
  --text-3: #A0AEC0;        /* 标签/占位 */

  /* 边框与表面 */
  --border: #E2E8F0;
  --border-strong: #CBD5E0;
  --surface: rgba(255,255,255,0.80);
  --surface-hover: rgba(238,242,247,0.90);

  /* 圆角 */
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 24px;

  /* 阴影 */
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.06);
  --shadow-md: 0 4px 16px rgba(0,0,0,0.08);
  --shadow-lg: 0 12px 40px rgba(0,0,0,0.12);

  /* 缓动 */
  --ease: cubic-bezier(0.4,0,0.2,1);
  --ease-bounce: cubic-bezier(0.34,1.56,0.64,1);

  /* 字体 */
  --font-cn: "HarmonyOS Sans","Noto Sans SC","PingFang SC","Microsoft YaHei",sans-serif;
  --font-en: "Inter",-apple-system,sans-serif;
  --font-mono: "SF Mono","Fira Code","Courier New",monospace;
}
```

## 背景处理

明亮科技风不需要暗色光晕，改用微妙渐变和网格。

```css
body { background: var(--bg-0); color: var(--text-1); }
/* 顶部微妙渐变 */
.bg-gradient {
  position: fixed; top: 0; left: 0; right: 0; height: 400px; z-index: 0; pointer-events: none;
  background: linear-gradient(180deg, rgba(0,102,255,0.03) 0%, transparent 100%);
}
/* 可选：极淡网格 */
.bg-grid {
  position: fixed; inset: 0; z-index: 0; pointer-events: none;
  background-image: linear-gradient(rgba(0,102,255,0.02) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(0,102,255,0.02) 1px, transparent 1px);
  background-size: 48px 48px;
  mask-image: radial-gradient(ellipse 80% 60% at 50% 20%, black 30%, transparent 80%);
}
```

## Header

```css
.header {
  position: fixed; top: 0; left: 0; right: 0; height: 64px; z-index: 1000;
  background: rgba(255,255,255,0.85);
  backdrop-filter: saturate(180%) blur(20px);
  -webkit-backdrop-filter: saturate(180%) blur(20px);
  border-bottom: 1px solid var(--border);
}
```

## 卡片

```css
.card {
  background: var(--bg-1);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 24px;
  box-shadow: var(--shadow-sm);
  transition: all 0.3s var(--ease);
}
.card:hover {
  border-color: var(--border-strong);
  box-shadow: var(--shadow-md);
  transform: translateY(-2px);
}
```

## 按钮

```css
.btn-primary {
  background: var(--accent);
  color: #fff;
  box-shadow: 0 1px 3px rgba(0,102,255,0.20);
}
.btn-primary:hover {
  background: #0052D9;
  box-shadow: 0 4px 16px rgba(0,102,255,0.25);
  transform: translateY(-1px);
}
.btn-ghost {
  border: 1px solid var(--border);
  color: var(--text-1);
}
.btn-ghost:hover {
  border-color: var(--accent);
  background: var(--accent-glow);
  color: var(--accent);
}
```

## 表单

```css
.form-input {
  background: var(--bg-0);
  border: 1px solid var(--border);
  color: var(--text-0);
}
.form-input:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px var(--accent-glow);
}
.form-input::placeholder { color: var(--text-3); }
```

## Modal

```css
.modal-overlay { background: rgba(26,32,44,0.40); backdrop-filter: blur(4px); }
.modal-box {
  background: var(--bg-0);
  border: 1px solid var(--border);
  box-shadow: var(--shadow-lg);
}
.modal-head { border-bottom: 1px solid var(--border); }
.modal-foot { border-top: 1px solid var(--border); }
```

## 动画

```css
/* fade-up 入场 */
.fade-up { opacity: 0; transform: translateY(20px); transition: opacity 0.6s var(--ease), transform 0.6s var(--ease); }
.fade-up.visible { opacity: 1; transform: translateY(0); }

/* 按钮波纹 */
.btn-primary { position: relative; overflow: hidden; }
.btn-primary::after {
  content: ''; position: absolute; inset: 0;
  background: radial-gradient(circle at center, rgba(255,255,255,0.2), transparent 60%);
  opacity: 0; transition: opacity 0.3s;
}
.btn-primary:active::after { opacity: 1; }
```

## 适用场景与禁忌

- 适合：SaaS 产品界面、管理后台、文档站、数据看板
- 禁忌：不要使用大面积纯白无层次；阴影不可过重；不可使用荧光色

## 移动端适配

**断点规则**（在 SKILL.md 通用骨架基础上追加本风格专属规则）：

```css
/* ---- 平板 ---- */
@media (max-width: 1024px) {
  .card-grid { grid-template-columns: repeat(2, 1fr); gap: 12px; }
  .feature-section { padding: 48px 24px; }
}

/* ---- 移动端 ---- */
@media (max-width: 768px) {
  /* 卡片间距从 16px 降至 12px */
  .card-grid { grid-template-columns: 1fr; gap: 12px; }

  /* 阴影减轻（移动端浅色背景阴影更明显） */
  .card { box-shadow: 0 1px 4px rgba(0,0,0,0.06); }

  /* 微渐变背景简化 */
  .bg-gradient { background: var(--bg-1); }

  /* 表单标签和输入框纵向排列 */
  .form-row { flex-direction: column; align-items: stretch; }
  .form-row label { margin-bottom: 6px; }
}

/* ---- 小屏 ---- */
@media (max-width: 480px) {
  .card { padding: 16px; }
  .feature-section { padding: 32px 16px; }
  .btn-primary { width: 100%; }
}
```

**关键点**：明亮科技风本身布局简洁，移动端主要调整是网格降列和间距收紧。浅色背景在移动端阴影需要更轻（`0.06` 透明度），否则会显得脏。按钮在小屏全宽排列。
