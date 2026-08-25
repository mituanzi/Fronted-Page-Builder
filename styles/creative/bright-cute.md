# 明亮可爱风（Bright Cute）

> 参考：Duolingo、飞书、Lark、Notion 部分插画页

> 适用：教育产品、消费级应用、轻松向工具、引导页

## 配色体系

```css
:root {
  /* 底色层 — 暖白基底 */
  --bg-0: #FFF8F4;          /* 全局背景，暖白 */
  --bg-1: #FFFFFF;          /* 卡片白 */
  --bg-2: #FFF0EA;          /* 悬浮暖色 */
  --bg-3: #FFE4D9;          /* 边缘 */

  /* 主色调 — 活泼珊瑚 */
  --accent: #FF6B6B;         /* 珊瑚红 */
  --accent-glow: rgba(255,107,107,0.12);
  --accent-2: #4ECDC4;       /* 薄荷绿 */
  --accent-3: #FFD93D;       /* 阳光黄 */
  --accent-4: #A78BFA;       /* 薰衣草紫 */

  /* 语义色 */
  --success: #51CF66;
  --warning: #FFD93D;
  --danger: #FF6B6B;

  /* 文字层级 */
  --text-0: #2D2D2D;        /* 标题 */
  --text-1: #4A4A4A;        /* 正文 */
  --text-2: #888888;        /* 次要 */
  --text-3: #B0B0B0;        /* 标签 */

  /* 边框与表面 */
  --border: #FFE4D9;
  --border-strong: #FFCBA8;
  --surface: rgba(255,255,255,0.90);
  --surface-hover: rgba(255,240,234,0.95);

  /* 圆角 — 大圆角为主 */
  --radius-sm: 12px;
  --radius-md: 16px;
  --radius-lg: 24px;
  --radius-xl: 32px;
  --radius-full: 999px;

  /* 阴影 — 柔和、有色调 */
  --shadow-sm: 0 2px 8px rgba(255,107,107,0.06);
  --shadow-md: 0 8px 24px rgba(255,107,107,0.10);
  --shadow-lg: 0 16px 48px rgba(255,107,107,0.15);

  /* 缓动 — 弹性为主 */
  --ease: cubic-bezier(0.4,0,0.2,1);
  --ease-bounce: cubic-bezier(0.34,1.56,0.64,1);

  /* 字体 */
  --font-cn: "HarmonyOS Sans","Noto Sans SC","PingFang SC",sans-serif;
  --font-en: "Inter",-apple-system,sans-serif;
}
```

## 背景处理

```css
body { background: var(--bg-0); color: var(--text-1); }
/* 柔和渐变光斑 */
.bg-blob-1 {
  position: fixed; top: -100px; right: -100px; width: 400px; height: 400px; z-index: 0; pointer-events: none;
  background: radial-gradient(circle, rgba(255,107,107,0.08), transparent 70%);
  border-radius: 50%;
  animation: blobFloat 16s ease-in-out infinite;
}
.bg-blob-2 {
  position: fixed; bottom: -100px; left: -100px; width: 500px; height: 500px; z-index: 0; pointer-events: none;
  background: radial-gradient(circle, rgba(78,205,196,0.06), transparent 70%);
  border-radius: 50%;
  animation: blobFloat 20s ease-in-out infinite reverse;
}
@keyframes blobFloat {
  0%,100% { transform: translate(0,0) scale(1) }
  33% { transform: translate(30px,-20px) scale(1.05) }
  66% { transform: translate(-20px,30px) scale(0.95) }
}
```

## Header

```css
.header {
  position: fixed; top: 0; left: 0; right: 0; height: 60px; z-index: 1000;
  background: rgba(255,248,244,0.90);
  backdrop-filter: blur(16px);
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
  transition: all 0.3s var(--ease-bounce);
}
.card:hover {
  box-shadow: var(--shadow-md);
  transform: translateY(-4px) scale(1.01);
}
```

## 按钮

```css
.btn-primary {
  background: var(--accent);
  color: #fff;
  border-radius: var(--radius-full);
  padding: 12px 32px;
  font-weight: 600;
  box-shadow: 0 4px 12px rgba(255,107,107,0.20);
}
.btn-primary:hover {
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 8px 24px rgba(255,107,107,0.30);
}
.btn-primary:active {
  transform: translateY(0) scale(0.98);
}
.btn-ghost {
  border: 2px solid var(--border-strong);
  color: var(--text-1);
  border-radius: var(--radius-full);
}
.btn-ghost:hover {
  border-color: var(--accent);
  background: var(--accent-glow);
}
```

## 表单

```css
.form-input {
  background: var(--bg-1);
  border: 2px solid var(--border);
  color: var(--text-0);
  border-radius: var(--radius-md);
}
.form-input:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 4px var(--accent-glow);
}
.form-input::placeholder { color: var(--text-3); }
```

## Modal

```css
.modal-overlay { background: rgba(45,45,45,0.30); backdrop-filter: blur(6px); }
.modal-box {
  background: var(--bg-1);
  border: 2px solid var(--border);
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-lg);
}
```

## 特色动画

```css
/* 弹跳入场 */
.fade-up { opacity: 0; transform: translateY(24px) scale(0.95); transition: all 0.5s var(--ease-bounce); }
.fade-up.visible { opacity: 1; transform: translateY(0) scale(1); }

/* 图标摇摆 */
@keyframes wiggle {
  0%,100% { transform: rotate(0deg) }
  25% { transform: rotate(-8deg) }
  75% { transform: rotate(8deg) }
}
.icon-cute:hover { animation: wiggle 0.5s ease-in-out; }

/* 按钮脉动 */
@keyframes pulse-cute {
  0%,100% { box-shadow: 0 4px 12px rgba(255,107,107,0.20) }
  50% { box-shadow: 0 4px 24px rgba(255,107,107,0.40) }
}
.btn-pulse { animation: pulse-cute 2s ease-in-out infinite; }
```

## Emoji 使用建议

可爱风鼓励在以下位置使用 emoji：
- 卡片标题前缀（1 个 emoji + 文字）
- 空状态提示（大 emoji + 文字）
- Toast 通知开头（1 个 emoji）
- 按钮文字前缀（可选）
- 不在正文段落、表格数据、表单标签中使用

## 适用场景与禁忌

- 适合：教育产品、C 端消费应用、引导页、活动页、轻松向工具
- 禁忌：不可使用尖锐直角；阴影不可过重变成"压迫感"；不可使用深黑色文字（用 `#2D2D2D` 代替 `#000`）

## 移动端适配

**断点规则**（在 SKILL.md 通用骨架基础上追加本风格专属规则）：

```css
/* ---- 平板 ---- */
@media (max-width: 1024px) {
  .habit-grid { grid-template-columns: repeat(2, 1fr); }
  .stats-row { gap: 12px; }
}

/* ---- 移动端 ---- */
@media (max-width: 768px) {
  /* 大圆角从 32px 降至 20px（小屏过圆显得拥挤） */
  .card-cute, .modal-box { border-radius: 20px; }
  .btn-cute { border-radius: 16px; }

  /* 弹跳动画保留但更快（移动端注意力短） */
  .bounce-in { animation-duration: 0.3s; }
  .fade-up { transition: all 0.3s var(--ease-bounce); }

  /* Emoji 字号缩小 */
  .hero-emoji { font-size: 36px; }
  .icon-cute { font-size: 28px; }

  /* 习惯卡片单列 */
  .habit-grid { grid-template-columns: 1fr; }

  /* 统计卡片纵向 */
  .stats-row { flex-direction: column; }
  .stat-card { min-width: auto; width: 100%; }

  /* 渐变光斑缩小 */
  .bg-blob-1, .bg-blob-2 { width: 200px; height: 200px; opacity: 0.4; }
}

/* ---- 小屏 ---- */
@media (max-width: 480px) {
  .hero-title { font-size: 22px; }
  .card-cute { padding: 16px; border-radius: 16px; }
  .btn-cute { width: 100%; }
  .emoji-celebrate { font-size: 48px; }
}
```

**关键点**：可爱风在移动端保持圆润和弹跳感，但大圆角需从 32px 降至 20px（小屏过大圆角会压缩内容空间）。弹跳动画保留但缩短至 0.3s（移动端用户注意力更短）。Emoji 字号适当缩小。渐变光斑减小并降低透明度。
