# 新粗野主义风（Neobrutalism）

> 参考：Gumroad、Bolt.new、Linear 部分页面、Figma Community、粗野主义网页设计潮流
> 适用：创意品牌、独立产品、设计工作室、开发者工具、个人作品集、活动页

## 配色体系

```css
:root {
  /* 底色层 — 高饱和明亮色 */
  --bg-0: #FFE600;          /* 全局背景，亮黄 */
  --bg-1: #FFFFFF;          /* 卡片白 */
  --bg-2: #FF6B6B;          /* 卡片红 */
  --bg-3: #4ECDC4;          /* 卡片青 */
  --bg-4: #A78BFA;          /* 卡片紫 */

  /* 主色 — 纯黑 */
  --accent: #000000;         /* 主色，纯黑 */
  --accent-glow: rgba(0,0,0,0.0);
  --accent-2: #FF3366;      /* 辅助高饱和粉红 */

  /* 语义色 */
  --success: #00C896;
  --warning: #FFAA00;
  --danger: #FF3366;

  /* 文字 — 纯黑为主 */
  --text-0: #000000;        /* 标题 */
  --text-1: #1A1A1A;        /* 正文 */
  --text-2: #333333;        /* 次要 */
  --text-3: #555555;        /* 标签 */

  /* 边框 — 粗黑边框是核心 */
  --border: #000000;
  --border-strong: #000000;

  /* 阴影 — 硬阴影（无模糊）是核心 */
  --shadow-sm: 2px 2px 0px #000000;
  --shadow-md: 4px 4px 0px #000000;
  --shadow-lg: 6px 6px 0px #000000;
  --shadow-xl: 8px 8px 0px #000000;

  /* 圆角 — 极小或无 */
  --radius-sm: 0px; --radius-md: 4px; --radius-lg: 8px; --radius-xl: 12px;

  /* 缓动 — 硬切，快速 */
  --ease: steps(4, end);
  --ease-fast: cubic-bezier(0.0,0.0,0.2,1);

  --header-h: 64px;
  --font-cn: "HarmonyOS Sans","Noto Sans SC","PingFang SC",sans-serif;
  --font-en: "Space Grotesk","Inter",-apple-system,sans-serif;
}
```

**设计原则**
- 粗黑边框（2-4px solid black）是灵魂，所有可见容器必须有边框
- 硬阴影（`Npx Npx 0px #000`，零模糊）替代柔阴影，阴影偏移量与元素大小成正比
- 高饱和底色大胆铺用：黄、红、青、紫、粉作为卡片背景色，不怕撞色
- 字体要大、要粗：标题 32-64px 且 font-weight 800+，正文 16-18px
- 动画要快、要硬：使用 `steps()` 或极短时长（0.15-0.2s），不要柔和缓动
- 圆角极小（0-8px），强调几何感和"方块感"

## 外部字体

```html
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">
```

## 背景处理

```css
body { background: var(--bg-0); color: var(--text-1); }

/* 不需要装饰性背景，高饱和纯色底就是背景 */
/* 可选：CSS 网格点阵 */
.bg-dots {
  background-image: radial-gradient(circle, #000000 1.5px, transparent 1.5px);
  background-size: 24px 24px;
}
```

## Header

```css
.header {
  position: fixed; top: 0; left: 0; right: 0; height: var(--header-h);
  background: var(--bg-0); border-bottom: 3px solid var(--border);
  z-index: 1000; display: flex; align-items: center; padding: 0 24px;
}
.header-title {
  font-family: var(--font-en); font-size: 22px; font-weight: 700;
  color: var(--text-0); text-transform: uppercase; letter-spacing: -0.5px;
}
```

## 卡片

```css
.card {
  background: var(--bg-1); border: 3px solid var(--border);
  border-radius: var(--radius-md); padding: 24px;
  box-shadow: var(--shadow-md);
  transition: all 0.15s var(--ease-fast);
}
.card:hover {
  transform: translate(-2px, -2px);
  box-shadow: var(--shadow-lg);
}

/* 彩色卡片变体 */
.card-red { background: var(--bg-2); color: #FFFFFF; }
.card-cyan { background: var(--bg-3); }
.card-purple { background: var(--bg-4); color: #FFFFFF; }

/* 彩色卡片中的文字颜色调整 */
.card-red .card-title, .card-purple .card-title { color: #FFFFFF; }
```

## 按钮

```css
/* 主按钮 — 黑底白字 + 硬阴影 */
.btn-primary {
  background: var(--accent); color: #FFFFFF;
  border: 3px solid var(--border); padding: 12px 28px;
  font-size: 16px; font-weight: 700; text-transform: uppercase;
  border-radius: var(--radius-md); cursor: pointer;
  box-shadow: var(--shadow-md);
  transition: all 0.15s var(--ease-fast);
}
.btn-primary:hover {
  transform: translate(-2px, -2px); box-shadow: var(--shadow-lg);
}
.btn-primary:active {
  transform: translate(2px, 2px); box-shadow: var(--shadow-sm);
}

/* 描边按钮 — 白底黑边 */
.btn-outline {
  background: var(--bg-1); color: var(--text-0);
  border: 3px solid var(--border); padding: 12px 28px;
  font-size: 16px; font-weight: 700; text-transform: uppercase;
  border-radius: var(--radius-md); cursor: pointer;
  box-shadow: var(--shadow-md);
  transition: all 0.15s var(--ease-fast);
}
.btn-outline:hover {
  transform: translate(-2px, -2px); box-shadow: var(--shadow-lg);
  background: var(--accent); color: #FFFFFF;
}
.btn-outline:active {
  transform: translate(2px, 2px); box-shadow: var(--shadow-sm);
}

/* 彩色按钮 */
.btn-red { background: var(--accent-2); color: #FFFFFF; border-color: #000000; }
.btn-cyan { background: var(--bg-3); color: #000000; border-color: #000000; }
```

## 表单

```css
.input, .select, .textarea {
  background: var(--bg-1); border: 3px solid var(--border);
  color: var(--text-0); padding: 10px 14px;
  border-radius: var(--radius-md); font-size: 16px; font-weight: 500;
  box-shadow: var(--shadow-sm);
  transition: all 0.15s var(--ease-fast);
}
.input:focus, .select:focus, .textarea:focus {
  outline: none; box-shadow: var(--shadow-md);
  transform: translate(-1px, -1px);
}
.input::placeholder { color: var(--text-3); font-weight: 400; }

/* 标签 — 粗边框徽章 */
.tag-brutal {
  display: inline-block; padding: 4px 12px; font-size: 13px;
  font-weight: 700; text-transform: uppercase;
  border: 2px solid var(--border); background: var(--bg-1);
  border-radius: var(--radius-sm);
}
.tag-brutal-red { background: var(--accent-2); color: #FFFFFF; }
.tag-brutal-cyan { background: var(--bg-3); }
```

## Modal 样式

```css
.modal-overlay { background: rgba(0,0,0,0.50); }
.modal-box {
  background: var(--bg-1); border: 4px solid var(--border);
  box-shadow: var(--shadow-xl); border-radius: var(--radius-lg);
}
.modal-head { border-bottom: 3px solid var(--border); }
.modal-foot { border-top: 3px solid var(--border); }
```

## 特色动画

```css
/* 硬切入场 — 步进式 */
@keyframes brutalIn {
  0% { opacity: 0; transform: translate(12px, 12px); }
  100% { opacity: 1; transform: translate(0, 0); }
}
.brutal-in { animation: brutalIn 0.2s var(--ease) forwards; }

/* 按压弹跳 — 活跃态 */
@keyframes brutalPress {
  0% { transform: translate(0, 0); }
  50% { transform: translate(4px, 4px); }
  100% { transform: translate(2px, 2px); }
}

/* 闪烁高亮 — 用于强调 */
@keyframes brutalBlink {
  0%,100% { background: var(--bg-1); }
  50% { background: var(--accent-2); color: #FFFFFF; }
}
.blink { animation: brutalBlink 0.5s steps(2) infinite; }
```

## 适用场景与禁忌

- 适合：创意品牌、独立产品官网、开发者工具、设计工作室、个人作品集、活动页、Z 世代产品
- 禁忌：不可使用柔阴影（`box-shadow` 模糊半径必须为 0）；不可使用柔和缓动曲线（用 `steps()` 或线性）；不可使用大圆角（>12px）；不可使用低饱和度颜色（所有颜色必须高饱和）；不可使用浅灰色文字（用纯黑或深黑）；不可使用细边框（至少 2px，推荐 3px）

## 移动端适配

**断点规则**（在 SKILL.md 通用骨架基础上追加本风格专属规则）：

```css
/* ---- 平板 ---- */
@media (max-width: 1024px) {
  .brut-grid { grid-template-columns: repeat(2, 1fr); }
}

/* ---- 移动端 ---- */
@media (max-width: 768px) {
  /* 硬阴影从 4px 降至 3px（小屏减少视觉压迫） */
  .brut-card { box-shadow: 3px 3px 0px #000; }
  .brut-btn { box-shadow: 3px 3px 0px #000; }

  /* 边框从 3px 降至 2px（小屏节省空间） */
  .brut-card, .brut-btn { border-width: 2px; }

  /* 保持 0 圆角（粗野主义核心特征不可妥协） */
  /* 圆角不做任何调整，维持 0-4px */

  /* 网格单列 */
  .brut-grid { grid-template-columns: 1fr; }

  /* 大标题保持冲击力但不溢出 */
  .brut-title { font-size: 36px; word-break: break-word; }

  /* 按钮全宽 */
  .brut-btn { width: 100%; }
}

/* ---- 小屏 ---- */
@media (max-width: 480px) {
  .brut-title { font-size: 28px; }
  .brut-card { padding: 16px; }
  /* 阴影进一步缩小但保持可见 */
  .brut-card { box-shadow: 2px 2px 0px #000; }
}
```

**关键点**：新粗野主义在移动端的核心矛盾是"视觉冲击 vs 小屏空间"。解决方案：硬阴影从 4px 降至 3px（小屏仍可见但不压迫），边框从 3px 降至 2px（节省空间），但圆角保持 0px（核心特征不可妥协）。标题用 `word-break: break-word` 防止长标题溢出。
