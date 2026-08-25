# 深色工业科技风（Industrial Dark）

> 参考：AI 预测引擎、数据平台、监控大屏
> 适用：数据平台、科研工具、企业内部系统、预测引擎、管理后台

## 配色体系

采用"深色底 + 双色主调 + 语义色"的三层配色架构。

**底色层（从深到浅）**
```
--bg-0: #081018   /* 全局背景，最深 */
--bg-1: #0B1828   /* 卡片背景 */
--bg-2: #102A43   /* 悬浮/嵌套背景 */
--bg-3: #15314F   /* 边缘/分隔 */
```

**主色调（双色互补）**
```
--ai-cyan: #00C8D7     /* 主交互色，用于链接、激活、主按钮 */
--ai-purple: #7567FF   /* 辅助强调色，用于渐变、标签、次要交互 */
```

**语义色**
```
--cnpc-red: #C40018    /* 品牌/警示/错误 */
--ai-green: #5B8C5A    /* 成功/正向 */
```

**文字层级（从亮到暗）**
```
--text-0: #F0F4F8   /* 标题、关键数据 */
--text-1: #C4D0DE   /* 正文 */
--text-2: #8295A8   /* 次要说明 */
--text-3: #5A6E82   /* 标签、占位、时间戳 */
```

**边框与表面**
```
--border: rgba(0,200,215,0.12)        /* 常规边框，低透明度主色 */
--border-strong: rgba(0,200,215,0.28) /* 强调边框，hover/激活态 */
--surface: rgba(16,42,67,0.55)        /* 半透明卡片表面 */
--surface-hover: rgba(20,52,80,0.7)   /* 悬浮态 */
```

**完整 :root 变量**
```css
:root {
  --bg-0: #081018; --bg-1: #0B1828; --bg-2: #102A43; --bg-3: #15314F;
  --ai-cyan: #00C8D7; --ai-purple: #7567FF;
  --cnpc-red: #C40018; --ai-green: #5B8C5A;
  --accent: var(--ai-cyan); --accent-glow: rgba(0,200,215,0.10);
  --accent-2: var(--ai-purple);
  --success: #5B8C5A; --warning: #C40018; --danger: #C40018;
  --text-0: #F0F4F8; --text-1: #C4D0DE; --text-2: #8295A8; --text-3: #5A6E82;
  --border: rgba(0,200,215,0.12); --border-strong: rgba(0,200,215,0.28);
  --surface: rgba(16,42,67,0.55); --surface-hover: rgba(20,52,80,0.7);
  --radius-sm: 8px; --radius-md: 12px; --radius-lg: 16px; --radius-xl: 24px;
  --shadow-sm: 0 2px 8px rgba(0,0,0,0.3); --shadow-md: 0 8px 32px rgba(0,0,0,0.4); --shadow-lg: 0 16px 48px rgba(0,0,0,0.5);
  --ease: cubic-bezier(0.4,0,0.2,1); --ease-bounce: cubic-bezier(0.34,1.56,0.64,1);
  --header-h: 68px;
  --font-cn: "HarmonyOS Sans","Noto Sans SC","Source Han Sans SC","PingFang SC","Microsoft YaHei",sans-serif;
  --font-en: "Inter",-apple-system,sans-serif;
  --font-mono: "Courier New",monospace;
}
```

**设计原则**
- 主色 `--ai-cyan` 仅用于交互元素和关键数据，不要大面积铺色
- 边框一律使用主色的低透明度 rgba，营造"发丝"感而非实线
- 文字必须保持 4 级层级，通过明度差异引导视觉焦点
- 品牌色（红）克制使用，仅用于 logo 区、错误状态、关键徽标

## 玻璃态效果

```css
.glass {
  background: var(--surface);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid var(--border);
  border-radius: 16px;
}
```

**使用场景**：卡片、Modal、下拉面板、浮动条
**注意**：`backdrop-filter` 在低端设备性能较差，页面内同时使用不超过 8 个玻璃态元素

## 动画规范

**缓动函数**
```css
--ease: cubic-bezier(0.4, 0, 0.2, 1);          /* 标准缓动 */
--ease-bounce: cubic-bezier(0.34, 1.56, 0.64, 1); /* 弹性缓动 */
```

**入场动画：fade-up**
```css
.fade-up {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.8s var(--ease), transform 0.8s var(--ease);
}
.fade-up.visible {
  opacity: 1;
  transform: translateY(0);
}
```
配合 IntersectionObserver，元素进入视口时添加 `.visible` 类。多个元素设置 `transition-delay` 实现错落入场。

**呼吸动画：breathe**
```css
.breathe { animation: breathe 3s ease-in-out infinite; }
@keyframes breathe {
  0%, 100% { box-shadow: 0 0 12px rgba(0,200,215,0.15); }
  50% { box-shadow: 0 0 24px rgba(0,200,215,0.35); }
}
```
用于关键按钮或图标的持续注意力引导。

**背景光晕：floatGlow**
```css
.bg-glow-1 {
  position: fixed; top: -200px; left: -100px;
  width: 600px; height: 600px;
  z-index: 0; pointer-events: none;
  background: radial-gradient(circle, rgba(0,200,215,0.08), transparent 70%);
  animation: floatGlow 14s ease-in-out infinite;
}
@keyframes floatGlow {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(40px, 30px); }
}
```
页面背景放置 2-3 个不同颜色、不同周期的光晕，营造空间深度。

**网格背景**
```css
.bg-grid {
  position: fixed; inset: 0; z-index: 0; pointer-events: none;
  background-image: linear-gradient(rgba(0,200,215,0.03) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(0,200,215,0.03) 1px, transparent 1px);
  background-size: 48px 48px;
  mask-image: radial-gradient(ellipse 80% 60% at 50% 30%, black 30%, transparent 80%);
}
```

**按钮波纹**
```css
.btn-primary { position: relative; overflow: hidden; }
.btn-primary::after {
  content: ''; position: absolute; inset: 0;
  background: radial-gradient(circle at var(--rx, 50%) var(--ry, 50%), rgba(255,255,255,0.3), transparent 50%);
  opacity: 0; transition: opacity 0.4s;
}
.btn-primary:active::after { opacity: 1; }
```

**数字递增动画**
```javascript
function animateCountTo(el, target, duration) {
  var start = 0;
  var startTime = null;
  function tick(ts) {
    if (!startTime) startTime = ts;
    var progress = Math.min((ts - startTime) / duration, 1);
    var eased = 1 - Math.pow(1 - progress, 3); // easeOutCubic
    el.textContent = Math.round(start + (target - start) * eased);
    if (progress < 1) requestAnimationFrame(tick);
  }
  requestAnimationFrame(tick);
}
```

**Loading 进度条**
```css
.ml-prog { width: 100%; height: 4px; background: var(--surface-hover); border-radius: 2px; overflow: hidden; }
.ml-prog-fill { height: 100%; background: linear-gradient(90deg, var(--ai-cyan), var(--ai-purple)); width: 0%; transition: width 0.3s var(--ease); border-radius: 2px; }
```
配合 JS 分阶段更新进度百分比（10% → 30% → 60% → 90% → 100%），每阶段间隔 200-400ms。

## 布局模式

**全局布局**
- Header 固定顶部（`position: fixed; top: 0`），高度 68px（`--header-h`）
- 主内容区 `padding-top: var(--header-h)`，最大宽度 1280px 居中
- 每个内容区块为 `<section>`，纵向间距 80-120px
- Footer 固定底部信息栏

**场景卡片网格**
```css
.scenario-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}
@media (max-width: 768px) { .scenario-grid { grid-template-columns: 1fr; } }
```

**响应式断点**
- `> 1024px`：桌面完整布局
- `768px - 1024px`：网格 2 列 → 1 列
- `< 768px`：单列，Modal 全宽
- `< 640px`：紧凑间距，表单单列

## 字体规范

```css
--font-cn: "HarmonyOS Sans", "Noto Sans SC", "Source Han Sans SC", "PingFang SC", "Microsoft YaHei", sans-serif;
--font-en: "Inter", -apple-system, sans-serif;
```
- 中文使用 HarmonyOS Sans / Noto Sans SC 系列
- 英文/数字使用 Inter
- 等宽场景（代码、SMILES）使用 `'Courier New', monospace`
- 正文 14px，标题 24-48px，标签 11-12px（大写 + letter-spacing）

## Header 布局

```html
<header class="header">
  <div class="header-left">
    <span class="h-title">页面标题</span>
    <span class="h-sub">ENGLISH SUBTITLE</span>
  </div>
  <div class="header-right">
    <!-- 功能按钮组（38x38 圆角方块）+ 用户信息条 -->
  </div>
</header>
```
- 左侧：中文标题 + 英文副标题
- 右侧：功能图标按钮（38x38px，8px 圆角）+ 用户头像条
- 背景：`rgba(8,16,24,0.85) + backdrop-filter: blur(20px)`
- 底部 1px 发丝边框

## 按钮体系

```css
.btn-primary {
  background: linear-gradient(135deg, var(--ai-cyan), var(--ai-purple));
  color: #fff; border: none;
  padding: 12px 28px; border-radius: 10px;
  font-size: 14px; font-weight: 500; cursor: pointer;
  transition: all 0.3s var(--ease);
}
.btn-primary:hover { transform: translateY(-1px); box-shadow: 0 8px 24px rgba(0,200,215,0.25); }

.btn-ghost {
  background: transparent; border: 1px solid var(--border); color: var(--text-1);
  padding: 12px 28px; border-radius: 10px; cursor: pointer; transition: all 0.3s var(--ease);
}
.btn-ghost:hover { border-color: var(--border-strong); background: var(--surface-hover); }
```

## 表单组件

```css
.form-input {
  width: 100%; padding: 12px 16px;
  background: var(--surface-2); border: 1px solid var(--border);
  border-radius: 10px; color: var(--text-0); font-size: 14px; font-family: inherit;
  outline: none; transition: border-color 0.2s;
}
.form-input:focus { border-color: var(--ai-cyan); box-shadow: 0 0 0 3px rgba(0,200,215,0.08); }

.batch-textarea {
  width: 100%; min-height: 120px; padding: 12px 16px;
  background: var(--surface-2); border: 1px solid var(--border); border-radius: 10px;
  color: var(--text-0); font-family: 'Courier New', monospace; font-size: 13px;
  resize: vertical; outline: none; transition: border-color 0.2s; line-height: 1.6;
}

.ind-chip {
  padding: 6px 14px; border-radius: 8px; font-size: 12px;
  border: 1px solid var(--border); background: var(--surface-2);
  color: var(--text-2); cursor: pointer; transition: all 0.2s; user-select: none;
}
.ind-chip.active {
  border-color: var(--ai-cyan); background: rgba(0,200,215,0.1); color: var(--ai-cyan);
}
```

## Modal 样式

```css
.modal-overlay { background: rgba(4,10,18,0.78); backdrop-filter: blur(8px); }
.modal-box { background: linear-gradient(180deg, var(--bg-1), var(--bg-2)); border: 1px solid var(--border); box-shadow: 0 24px 80px rgba(0,0,0,0.5); }
.modal-head { border-bottom: 1px solid var(--border); }
.modal-foot { border-top: 1px solid var(--border); }
```

## 结果展示

```css
.res-card { background: var(--surface-2); border: 1px solid var(--border); border-radius: 12px; padding: 20px; }
.res-item { display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid var(--border); }
.res-item:last-child { border-bottom: none; }

.batch-stat { background: var(--surface-2); border: 1px solid var(--border); border-radius: 10px; padding: 12px 18px; flex: 1; min-width: 120px; }
.batch-stat .bs-val { font-size: 22px; font-weight: 700; color: var(--text-0); font-family: var(--font-en); }
.batch-stat .bs-lbl { font-size: 11px; color: var(--text-3); margin-top: 2px; text-transform: uppercase; letter-spacing: 0.3px; }
```

## 适用场景与禁忌

- 适合：数据平台、科研工具、企业内部系统、预测引擎、管理后台、监控大屏
- 禁忌：不可使用纯白底；阴影不可过轻失去层次感；不可使用大面积荧光色；不可使用大圆角（>24px）

## 参考实现

完整参考：`/home/bml/xdg_root/workspace/ai4s-platform.html`（3,306 行）
