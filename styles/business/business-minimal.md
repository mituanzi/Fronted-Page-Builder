# 商务简约风（Business Minimal）

> 参考：Linear、Vercel、GitHub、Arco Design Pro

> 适用：企业内部系统、项目管理工具、开发者工具、数据 API 平台

## 配色体系

```css
:root {
  /* 底色层 — 纯净灰白 */
  --bg-0: #FAFAFA;          /* 全局背景 */
  --bg-1: #FFFFFF;          /* 卡片 */
  --bg-2: #F4F4F5;          /* 悬浮 */
  --bg-3: #E4E4E7;          /* 边缘 */

  /* 主色调 — 克制单色 */
  --accent: #18181B;         /* 近黑作为主色 */
  --accent-glow: rgba(24,24,27,0.06);
  --accent-2: #3B82F6;       /* 蓝色仅用于链接/强调 */

  /* 语义色 */
  --success: #22C55E;
  --warning: #F59E0B;
  --danger: #EF4444;

  /* 文字层级 */
  --text-0: #18181B;        /* 标题 */
  --text-1: #3F3F46;        /* 正文 */
  --text-2: #71717A;        /* 次要 */
  --text-3: #A1A1AA;        /* 标签 */

  /* 边框与表面 */
  --border: #E4E4E7;
  --border-strong: #D4D4D8;
  --surface: rgba(255,255,255,0.90);
  --surface-hover: rgba(244,244,245,0.90);

  /* 圆角 — 小圆角，克制 */
  --radius-sm: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;

  /* 阴影 — 极轻 */
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.04);
  --shadow-md: 0 2px 8px rgba(0,0,0,0.06);
  --shadow-lg: 0 8px 24px rgba(0,0,0,0.08);

  /* 缓动 */
  --ease: cubic-bezier(0.4,0,0.2,1);
  --ease-bounce: cubic-bezier(0.34,1.56,0.64,1);

  /* 字体 */
  --font-cn: "HarmonyOS Sans","Noto Sans SC","PingFang SC",sans-serif;
  --font-en: "Inter",-apple-system,sans-serif;
  --font-mono: "SF Mono","JetBrains Mono","Fira Code","Courier New",monospace;
}
```

## 背景处理

商务简约风背景极度克制，不加渐变光斑，不加网格。

```css
body { background: var(--bg-0); color: var(--text-1); }
/* 无额外背景装饰，靠分割线和留白营造层次 */
```

## Header

```css
.header {
  position: fixed; top: 0; left: 0; right: 0; height: 56px; z-index: 1000;
  background: var(--bg-1);
  border-bottom: 1px solid var(--border);
}
/* 无 blur，无透明，实色 */
```

## 卡片

```css
.card {
  background: var(--bg-1);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 24px;
  transition: border-color 0.2s var(--ease);
}
.card:hover {
  border-color: var(--border-strong);
}
/* 不加 translateY，不加 shadow 变化，极度克制 */
```

## 按钮

```css
.btn-primary {
  background: var(--accent);
  color: #fff;
  border-radius: var(--radius-md);
}
.btn-primary:hover { background: #27272A; }
.btn-ghost {
  border: 1px solid var(--border);
  color: var(--text-1);
  background: var(--bg-1);
}
.btn-ghost:hover { border-color: var(--border-strong); background: var(--bg-2); }
```

## 表单

```css
.form-input {
  background: var(--bg-1);
  border: 1px solid var(--border);
  color: var(--text-0);
  border-radius: var(--radius-md);
}
.form-input:focus {
  border-color: var(--accent-2);
  box-shadow: 0 0 0 3px rgba(59,130,246,0.08);
}
```

## Modal

```css
.modal-overlay { background: rgba(24,24,27,0.50); }
.modal-box {
  background: var(--bg-1);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
}
```

## 动画

```css
/* 极简入场 */
.fade-up { opacity: 0; transform: translateY(12px); transition: opacity 0.4s var(--ease), transform 0.4s var(--ease); }
.fade-up.visible { opacity: 1; transform: translateY(0); }
/* 不使用 bounce，不使用 scale，保持克制 */
```

## 排版规范

- 标题字号阶梯：32px → 24px → 20px → 16px → 14px
- 行高：标题 1.3，正文 1.6
- 段间距：16px
- 用分隔线（`border-bottom`）代替阴影做层次区分
- 标签/计数使用 `font-variant-numeric: tabular-nums` 等宽数字

## 适用场景与禁忌

- 适合：企业内部系统、项目管理、开发者工具、API 平台、文档站
- 禁忌：不可使用渐变背景；不可使用大圆角（>16px）；不可使用过重阴影；不可使用 emoji

## 移动端适配

**断点规则**（在 SKILL.md 通用骨架基础上追加本风格专属规则）：

```css
/* ---- 平板 ---- */
@media (max-width: 1024px) {
  .content-wrapper { max-width: 800px; }
  .feature-grid { grid-template-columns: repeat(2, 1fr); }
}

/* ---- 移动端 ---- */
@media (max-width: 768px) {
  /* 间距从 24px 降至 16px */
  .section { padding: 32px 16px; }
  .content-wrapper { padding: 0 16px; }

  /* 网格单列 */
  .feature-grid { grid-template-columns: 1fr; }

  /* 表单元素纵向 */
  .form-inline { flex-direction: column; gap: 12px; }

  /* 表格水平滚动 */
  .table-wrapper { overflow-x: auto; }
  .data-table { min-width: 500px; }

  /* Header 简化：仅保留 logo + 汉堡菜单 */
  .header-right .header-secondary { display: none; }
}

/* ---- 小屏 ---- */
@media (max-width: 480px) {
  .section { padding: 24px 12px; }
  .feature-grid { gap: 12px; }
  .card { padding: 16px; }
  .btn-primary, .btn-secondary { width: 100%; }
}
```

**关键点**：商务简约风本身极简，移动端适配较为直接 — 主要是间距压缩和网格降列。此风格通常用于内部系统，表格水平滚动是主要的移动端交互方式。无需额外的视觉调整，保持克制即可。
