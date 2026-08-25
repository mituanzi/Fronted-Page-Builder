---
name: frontend-page-builder
description: |
  多风格前端页面构建 Skill。从润滑材料AI预测引擎项目沉淀，并扩展为十种风格的通用前端构建经验。
  覆盖设计体系、组件模式、交互逻辑、验证流程、工程规范。
  十种风格：深色工业科技、未来赛博、明亮科技、玻璃拟态、Apple极简、明亮可爱、新粗野主义、商务简约、数据仪表盘、国风雅致。
  触发条件：用户说"做个页面"、"前端页面"、"构建页面"、"build a page"、"做个UI"，或指定风格如"深色科技风"、"玻璃拟态"、"赛博朋克"、"Apple风格"、"可爱风"、"商务风"、"国风"时触发。
  也适用于：用户提供截图/设计稿要求复刻为前端页面、要求复用之前的页面风格。
  不适用于：需要 React/Vue/Next.js 框架的项目、纯移动端原生页面、需要 SSR 的场景。
---

# Frontend Page Builder — 多风格前端页面构建 Skill

> 从润滑材料AI预测引擎项目沉淀，并扩展为十种风格的通用前端构建经验。
> 覆盖设计体系、组件模式、交互逻辑、验证流程、工程规范。
> 适用于：需要快速搭建单页应用（SPA）的场景，纯 HTML+CSS+JS，无需构建工具。

## 触发条件

- 用户说"做个页面"、"前端页面"、"构建页面"、"build a page"、"做个UI"时触发
- 用户指定风格："深色科技风"、"玻璃拟态"、"赛博朋克"、"Apple风"、"可爱风"、"商务风"、"国风"时触发
- 用户要求复用"之前那个页面风格"时触发
- 用户提供截图/设计稿要求复刻为前端页面时触发
- 用户要求"用 frontend-page-builder"时触发

不适用于：需要 React/Vue/Next.js 框架的项目、纯移动端原生页面、需要 SSR 的场景。

---

## 风格路由器

根据用户描述自动选择风格预设，加载对应的风格文件：

| 用户关键词 | 风格 | 分类 | 风格文件 |
|---|---|---|---|
| 深色、科技、工业、酷炫、dashboard、监控大屏 | 深色工业科技风 | dark | `styles/dark/industrial-dark.md` |
| 赛博朋克、未来、霓虹、HUD、粒子、Web3、游戏 | 未来赛博风 | dark | `styles/dark/cyberpunk.md` |
| 明亮、清爽、Notion、Stripe、现代科技、SaaS | 明亮科技风 | modern | `styles/modern/bright-tech.md` |
| 玻璃拟态、毛玻璃、半透明、渐变光效、AI助手 | 玻璃拟态风 | modern | `styles/modern/glassmorphism.md` |
| Apple、极简、留白、超大标题、滚动动画、高端 | Apple 极简风 | modern | `styles/modern/apple-minimal.md` |
| 可爱、活泼、圆润、Duolingo、飞书、轻松 | 明亮可爱风 | creative | `styles/creative/bright-cute.md` |
| 粗野、新粗野主义、粗边框、高饱和、视觉冲击 | 新粗野主义 | creative | `styles/creative/neobrutalism.md` |
| 简约、克制、商务、Linear、Vercel、专业 | 商务简约风 | business | `styles/business/business-minimal.md` |
| 仪表盘、数据看板、侧边栏、图表、ERP、管理系统 | 数据仪表盘风 | business | `styles/business/dashboard.md` |
| 国风、水墨、雅致、传统、中国风、古风 | 国风雅致风 | cultural | `styles/cultural/chinese-elegant.md` |

**选择原则**：
- 用户未指定时，根据用途推断：数据平台→深色工业，AI产品→玻璃拟态，SaaS产品→明亮科技，产品官网→Apple极简，教育/消费→明亮可爱，创意品牌→新粗野主义，企业内部→商务简约，管理后台→数据仪表盘，文化展示→国风雅致
- 用户可混合风格（如"明亮但偏商务"），取主风格为基底，局部引用辅风格元素
- 匹配到风格后，**必须读取对应风格文件**获取完整设计体系

---

## 共享工程规范（所有风格通用）

### 单文件架构

HTML + CSS + JS 全部写在一个 `.html` 文件中，无需构建工具。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
  <title>页面标题 | English Title</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <style>
    /* 1. CSS Variables (:root) */ /* 2. Reset & Base */ /* 3. Background */
    /* 4. Header */ /* 5. Sections */ /* 6. Components */ /* 7. Forms */
    /* 8. Responsive (1024px + 768px + 480px 三档断点 + safe-area + 触摸优化) */
  </style>
</head>
<body>
  <!-- Background --><!-- Header --><!-- Main --><!-- Modals/Panels --><!-- Footer -->
  <script>
    /* 1. Config */ /* 2. Utils */ /* 3. Data */ /* 4. Modal */ /* 5. History */
    /* 6. Export */ /* 7. Detail */ /* 8. Dashboard */ /* 9. Init */
  </script>
</body>
</html>
```

### 外部依赖

- Google Fonts — 字体
- SmilesDrawer — 分子结构渲染（仅科研场景）
- 原则：外部依赖最多 2-3 个，CDN 必须锁版本号，不使用 jQuery/Bootstrap/Tailwind

### 代码风格

- 使用 `var` 而非 `let`/`const`
- 函数声明使用 `function name(){}`
- 字符串单引号，HTML 拼接用 `+=`
- 使用 `forEach` 而非 `for...of`
- 不使用 ES Modules / TypeScript

### localStorage 持久化

```javascript
var STORE_KEY = 'app_data';  // 统一命名：项目名_功能名
var MAX_RECORDS = 50;

function getData() {
  try { var s = localStorage.getItem(STORE_KEY); return s ? JSON.parse(s) : []; }
  catch (e) { return []; }
}

function saveData(item) {
  try {
    var list = getData();
    list.unshift(item);
    if (list.length > MAX_RECORDS) list = list.slice(0, MAX_RECORDS);
    localStorage.setItem(STORE_KEY, JSON.stringify(list));
    refreshAll();  // 触发所有依赖模块刷新
  } catch (e) { console.warn('Save failed:', e); }
}
```

### Mock 数据策略

```javascript
function mockPredict(indicators, seed) {
  var results = {};
  indicators.forEach(function(ind) {
    var range = ind.max - ind.min;
    var base = ind.min + range * (0.3 + Math.random() * 0.4);
    results[ind.key] = {
      value: base,
      confidence: 0.85 + Math.random() * 0.14,
      range: [base * 0.92, base * 1.08]
    };
  });
  return results;
}
```

### 验证流程

每次修改后必须执行：

1. **JS 语法校验**：提取 `<script>` 内容 → `node --check` 零错误
2. **括号平衡**：`{}`/`()`/`[]` 各自配对相等
3. **函数去重**：无重名函数（`tick` 嵌套作用域除外）
4. **HTML ID 完整性**：所有 `id="xxx"` 在 JS 中被引用
5. **onclick 绑定**：所有 `onclick="fn()"` 对应函数已定义
6. **文件记录**：行数 + 字节数

```bash
# 提取并校验
python3 -c "
import re
with open('page.html','r') as f: content = f.read()
scripts = re.findall(r'<script>(.*?)</script>', content, re.DOTALL)
for i, s in enumerate(scripts):
    with open(f'/tmp/check_{i}.js','w') as out: out.write(s)
"
node --check /tmp/check_0.js

python3 -c "
with open('/tmp/check_0.js','r') as f: js = f.read()
print('Braces:', js.count('{'), '/', js.count('}'))
print('Parens:', js.count('('), '/', js.count(')'))
print('Brackets:', js.count('['), '/', js.count(']'))
import re
from collections import Counter
funcs = re.findall(r'function\s+(\w+)\s*\(', js)
dupes = [n for n,c in Counter(funcs).items() if c>1]
print('Functions:', len(funcs), '| Duplicates:', dupes if dupes else 'None')
"
```

### 大文件编辑策略

- 小改动（<5 处）：直接使用 `edit` 工具
- 大改动（>=5 处）：编写 Python 脚本批量替换
- 每次修改后执行完整验证流程

---

## 共享组件模式（跨风格通用）

以下组件的 HTML 结构和 JS 逻辑跨风格通用，仅 CSS 变量值不同。各风格文件仅提供 CSS 变量差异。

### Modal 系统

```html
<div class="modal-overlay" id="modalOverlay" onclick="closeModal()"></div>
<div class="modal-box" id="modalBox">
  <div class="modal-head">
    <div class="m-icon" id="mIcon"></div>
    <div class="m-info"><div class="m-title" id="mTitle"></div><div class="m-sub" id="mSub"></div></div>
    <div class="m-close" onclick="closeModal()">&times;</div>
  </div>
  <div class="modal-body" id="modalForm"></div>
  <div class="modal-body modal-loading" id="modalLoading">
    <div class="ml-ring"></div><div class="ml-text" id="mlText">处理中...</div>
    <div class="ml-prog"><div class="ml-prog-fill" id="mlFill"></div></div>
  </div>
  <div class="modal-body modal-results" id="modalResults"></div>
  <div class="modal-foot" id="modalFoot">
    <button class="btn btn-ghost" onclick="closeModal()">关闭</button>
    <button class="btn btn-primary" id="btnSubmit" onclick="submit()">提交</button>
  </div>
</div>
```

**CSS 骨架**（各风格仅修改变量值）：
```css
.modal-overlay { position: fixed; inset: 0; z-index: 9000; opacity: 0; pointer-events: none; transition: opacity 0.3s var(--ease); }
.modal-overlay.show { opacity: 1; pointer-events: auto; }
.modal-box { position: fixed; top: 50%; left: 50%; transform: translate(-50%,-50%) scale(0.92); width: min(720px,92vw); max-height: 88vh; z-index: 9001; opacity: 0; pointer-events: none; transition: all 0.35s var(--ease); border-radius: var(--radius-lg); }
.modal-box.show { opacity: 1; pointer-events: auto; transform: translate(-50%,-50%) scale(1); }
```

### 侧滑面板

```css
.slide-panel { position: fixed; top: 0; right: -440px; width: 420px; height: 100vh; z-index: 9002; transition: right 0.35s var(--ease); display: flex; flex-direction: column; }
.slide-panel.show { right: 0; }
```

### 下拉菜单

```css
.dropdown { position: fixed; top: calc(var(--header-h) + 8px); right: 100px; width: 380px; z-index: 9102; opacity: 0; pointer-events: none; transform: translateY(-8px) scale(0.96); transition: all 0.25s var(--ease); border-radius: var(--radius-md); }
.dropdown.show { opacity: 1; pointer-events: auto; transform: translateY(0) scale(1); }
```

### Toast

```javascript
function showToast(msg) {
  var t = document.createElement('div');
  t.style.cssText = 'position:fixed;top:80px;right:28px;padding:12px 24px;border-radius:10px;font-size:14px;z-index:9999;transform:translateX(120%);transition:transform 0.4s var(--ease);max-width:400px';
  t.textContent = msg;
  document.body.appendChild(t);
  requestAnimationFrame(function() { t.style.transform = 'translateX(0)' });
  setTimeout(function() { t.style.transform = 'translateX(120%)'; setTimeout(function() { t.remove() }, 400) }, 3000);
}
```

### 按钮体系

```css
.btn-primary { padding: 12px 28px; border-radius: var(--radius-md); font-size: 14px; font-weight: 500; cursor: pointer; transition: all 0.3s var(--ease); border: none; }
.btn-ghost { padding: 12px 28px; border-radius: var(--radius-md); cursor: pointer; transition: all 0.3s var(--ease); background: transparent; }
```

### Tab 切换

```css
.tabs { display: flex; gap: 4px; border-radius: var(--radius-md); padding: 4px; }
.tab { flex: 1; padding: 10px 16px; text-align: center; border-radius: var(--radius-sm); cursor: pointer; transition: all 0.25s var(--ease); }
.tab.active { box-shadow: 0 2px 8px rgba(0,0,0,0.08); }
```

### 表单组件

```css
.form-input { width: 100%; padding: 12px 16px; border-radius: var(--radius-md); font-size: 14px; outline: none; transition: border-color 0.2s; }
.form-input:focus { box-shadow: 0 0 0 3px var(--accent-glow); }
.ind-chip { padding: 6px 14px; border-radius: var(--radius-sm); font-size: 12px; cursor: pointer; transition: all 0.2s; user-select: none; }
.ind-chip.active { border-color: var(--accent); background: var(--accent-glow); color: var(--accent); }
```

### 结果表格

```css
.data-table { width: 100%; border-collapse: collapse; }
.data-table th { padding: 10px 12px; text-align: left; font-size: 12px; border-bottom: 1px solid var(--border); text-transform: uppercase; letter-spacing: 0.3px; }
.data-table td { padding: 10px 12px; font-size: 13px; border-bottom: 1px solid var(--border); }
.data-table tbody tr { cursor: pointer; transition: background 0.15s; }
.data-table tbody tr:hover { background: var(--surface-hover); }
```

### CSV / Excel 导出

```javascript
function exportCSV(filename, headers, rows) {
  var BOM = '\ufeff';
  var csv = BOM + headers.join(',') + '\n' + rows.map(function(r) { return r.join(',') }).join('\n');
  var blob = new Blob([csv], { type: 'text/csv;charset=utf-8' });
  var a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = filename + '_' + Date.now() + '.csv';
  a.click();
}

function exportExcel(filename, headers, rows) {
  var html = '<html xmlns:x="urn:schemas-microsoft-com:office:excel"><head><meta charset="UTF-8"></head><body><table border="1"><tr>';
  headers.forEach(function(h) { html += '<th>' + h + '</th>' });
  html += '</tr>';
  rows.forEach(function(r) { html += '<tr>'; r.forEach(function(c) { html += '<td>' + c + '</td>' }); html += '</tr>' });
  html += '</table></body></html>';
  var blob = new Blob([html], { type: 'application/vnd.ms-excel' });
  var a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = filename + '_' + Date.now() + '.xls';
  a.click();
}
```

### 交互逻辑（跨风格通用）

**面板互斥**：打开任意面板时关闭其他
**ESC 优先级**：detail > assistant > notification > user-menu > history > modal
**IntersectionObserver**：fade-up 入场、图表懒加载
**数字递增动画**：requestAnimationFrame + easeOutCubic
**Loading 进度条**：分阶段推进 10% → 30% → 60% → 90% → 100%

### z-index 层级规范

```
Header: 1000
Modal overlay: 9000, box: 9001
侧滑 panel overlay: 9001, panel: 9002
Detail modal: 9002-9003
Dropdown overlay: 9101, panel: 9102
Toast: 9999
```

---

## 共享布局模式

### Bento Grid（模块化网格）

苹果近年流行的布局方式，信息密度高，视觉层次分明。可被任意风格复用。

```css
.bento-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(180px, auto);
  gap: 16px;
}
/* 大卡片占 2x2 */
.bento-lg { grid-column: span 2; grid-row: span 2; }
/* 宽卡片占 2x1 */
.bento-wide { grid-column: span 2; }
/* 高卡片占 1x2 */
.bento-tall { grid-row: span 2; }
/* 小卡片占 1x1（默认） */

@media (max-width: 1024px) {
  .bento-grid { grid-template-columns: repeat(2, 1fr); }
  .bento-lg { grid-column: span 2; grid-row: span 1; }
}
@media (max-width: 640px) {
  .bento-grid { grid-template-columns: 1fr; }
  .bento-lg, .bento-wide, .bento-tall { grid-column: span 1; grid-row: span 1; }
}
```

```html
<div class="bento-grid">
  <div class="bento-card bento-lg"><!-- 大卡片 --></div>
  <div class="bento-card"><!-- 小卡片 --></div>
  <div class="bento-card"><!-- 小卡片 --></div>
  <div class="bento-card bento-wide"><!-- 宽卡片 --></div>
  <div class="bento-card"><!-- 小卡片 --></div>
  <div class="bento-card"><!-- 小卡片 --></div>
</div>
```

**使用建议**：
- 主视觉/核心数据放大卡片
- 次要功能放小卡片
- 保持奇数个卡片（5/7/9）视觉更平衡
- 各风格文件中 `.bento-card` 的背景、边框、圆角由该风格的 CSS 变量决定

### Sidebar 布局

用于数据仪表盘、管理后台等需要持久导航的场景。

```css
.app-layout { display: flex; min-height: 100vh; }
.sidebar { width: 240px; flex-shrink: 0; }
.main-content { flex: 1; padding: 24px 32px; }

@media (max-width: 768px) {
  .app-layout { flex-direction: column; }
  .sidebar { width: 100%; height: auto; }
}
```

---

## 移动端自适应规范（所有风格必须实现）

> 每个生成的页面必须在桌面端和移动端都完整可用。以下规范为**强制要求**，生成页面时必须包含。

### 断点体系

采用三档断点，覆盖从大屏到小手机的全部设备：

| 断点 | 宽度范围 | 目标设备 | 核心变化 |
|---|---|---|---|
| 桌面 | > 1024px | PC / 大平板横屏 | 完整布局，多列网格 |
| 平板 | 769px - 1024px | iPad / Android 平板 | 网格降列，侧边栏可折叠 |
| 移动 | <= 768px | 手机竖屏 | 单列布局，汉堡菜单，底部导航 |
| 小屏 | <= 480px | 小手机 | 紧凑间距，字号缩小，表头吸顶 |

### CSS 自适应骨架（所有风格通用，生成时必须写入）

```css
/* ========== Responsive ========== */

/* ---- 平板断点 ---- */
@media (max-width: 1024px) {
  /* 网格降列 */
  .grid-2, .grid-3, .grid-4 { grid-template-columns: repeat(2, 1fr); }
  .bento-grid { grid-template-columns: repeat(2, 1fr); }
  .bento-lg { grid-column: span 2; grid-row: span 1; }
  /* 侧边栏折叠 */
  .sidebar { width: 64px; }
  .sidebar .sidebar-label { display: none; }
  .sidebar.expanded { width: 240px; }
  .sidebar.expanded .sidebar-label { display: block; }
  /* 主内容区缩窄 */
  .main-content { padding: 24px 24px; }
  /* 下拉面板缩窄 */
  .dropdown { width: min(340px, 90vw); }
}

/* ---- 移动端断点 ---- */
@media (max-width: 768px) {
  /* 基础间距 */
  .section { padding: 32px 16px; }
  .main-content { padding: 16px 16px; }

  /* Header 转汉堡菜单 */
  .header-nav { display: none; }
  .header-nav.mobile-open { display: flex; position: fixed; top: var(--header-h); left: 0; right: 0; flex-direction: column; background: var(--bg-1); padding: 16px; z-index: 1001; box-shadow: var(--shadow-md); gap: 8px; }
  .hamburger { display: flex; }

  /* 标题缩小 */
  .hero-title { font-size: 28px !important; }
  .section-title { font-size: 22px !important; }
  .hero-subtitle { font-size: 14px !important; }

  /* 网格全部单列 */
  .grid-2, .grid-3, .grid-4, .bento-grid, .scenario-grid, .mode-grid { grid-template-columns: 1fr; }
  .bento-lg, .bento-wide, .bento-tall { grid-column: span 1; grid-row: span 1; }

  /* Flex 纵向排列 */
  .stats-row, .agent-flow, .form-row, .batch-summary { flex-direction: column; gap: 12px; }
  .stat-card, .batch-stat { min-width: auto; width: 100%; }

  /* 侧边栏转底部导航 */
  .app-layout { flex-direction: column; }
  .sidebar { width: 100%; height: auto; position: fixed; bottom: 0; top: auto; flex-direction: row; overflow-x: auto; z-index: 1000; padding: 8px 0; padding-bottom: calc(8px + env(safe-area-inset-bottom)); }
  .sidebar .sidebar-item { flex-shrink: 0; }
  .main-content { padding-bottom: 80px; }

  /* Modal 全屏化 */
  .modal-box { width: 96vw; max-height: 92vh; border-radius: var(--radius-md); }
  .modal-body { padding: 16px; }

  /* 侧滑面板全屏 */
  .slide-panel { width: 100vw; right: -100vw; }
  .slide-panel.show { right: 0; }

  /* 下拉面板全宽 */
  .dropdown { width: calc(100vw - 32px); right: 16px; left: 16px; }

  /* 表格水平滚动 */
  .table-wrapper { overflow-x: auto; -webkit-overflow-scrolling: touch; }
  .data-table { min-width: 600px; }

  /* 隐藏次要信息 */
  .hide-mobile { display: none !important; }

  /* Toast 位置调整 */
  .toast { top: 72px; right: 16px; left: 16px; max-width: none; }
}

/* ---- 小屏断点 ---- */
@media (max-width: 480px) {
  .section { padding: 24px 12px; }
  .hero-title { font-size: 24px !important; }
  .hero-content { padding: 0; }
  .modal-box { width: 100vw; border-radius: 0; max-height: 100vh; }
  .modal-head { padding: 12px 16px; }
  .modal-body { padding: 12px; }
  .modal-foot { padding: 12px 16px; }
  .btn-primary, .btn-ghost { padding: 10px 20px; font-size: 14px; width: 100%; }
  .modal-foot { flex-direction: column; gap: 8px; }
  .modal-foot .btn-primary, .modal-foot .btn-ghost { width: 100%; }
}
```

### 汉堡菜单组件（移动端 Header 必备）

桌面端隐藏，移动端显示。点击展开/收起导航菜单。

```css
/* 汉堡按钮 — 桌面端隐藏 */
.hamburger {
  display: none;
  flex-direction: column;
  justify-content: center;
  gap: 5px;
  width: 38px; height: 38px;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: background 0.2s;
}
.hamburger span {
  display: block;
  width: 20px; height: 2px;
  background: var(--text-1);
  border-radius: 1px;
  transition: all 0.3s var(--ease);
}
.hamburger.active span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
.hamburger.active span:nth-child(2) { opacity: 0; }
.hamburger.active span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }
```

```html
<!-- 在 Header 中添加 -->
<div class="hamburger" onclick="toggleMobileNav()">
  <span></span><span></span><span></span>
</div>
```

```javascript
function toggleMobileNav() {
  var nav = document.querySelector('.header-nav');
  var btn = document.querySelector('.hamburger');
  nav.classList.toggle('mobile-open');
  btn.classList.toggle('active');
}
// 点击导航项后自动收起
document.querySelectorAll('.header-nav .nav-item').forEach(function(item) {
  item.addEventListener('click', function() {
    document.querySelector('.header-nav').classList.remove('mobile-open');
    document.querySelector('.hamburger').classList.remove('active');
  });
});
```

### 触摸优化规则

1. **最小点击区域 44x44px** — 所有可点击元素（按钮、链接、标签芯片）在移动端的最小尺寸为 44x44px（Apple HIG 标准）
```css
@media (max-width: 768px) {
  .btn-primary, .btn-ghost, .nav-item, .ind-chip, .tab {
    min-height: 44px;
    padding: 12px 20px;
  }
}
```

2. **禁用 hover 依赖** — 移动端没有 hover，关键操作不能只在 hover 中暴露
```css
@media (hover: none) {
  .hover-only { display: block; }  /* hover 才显示的元素改为常驻 */
  .desktop-tooltip { display: none; }  /* 桌面端 tooltip 在移动端隐藏 */
}
```

3. **禁用文本选择** — 按钮和导航项在移动端禁止长按选中
```css
@media (max-width: 768px) {
  .btn-primary, .btn-ghost, .nav-item, .hamburger, .tab {
    -webkit-user-select: none;
    user-select: none;
    -webkit-tap-highlight-color: transparent;
  }
}
```

### Safe Area 适配（刘海屏 / 底部安全区）

```css
/* Header 避让刘海 */
.header { padding-top: env(safe-area-inset-top); height: calc(var(--header-h) + env(safe-area-inset-top)); }

/* 底部导航避让 Home Indicator */
.bottom-nav, .sidebar { padding-bottom: env(safe-area-inset-bottom); }

/* Modal 全屏时避让 */
@media (max-width: 480px) {
  .modal-box { padding-top: env(safe-area-inset-top); padding-bottom: env(safe-area-inset-bottom); }
}
```

### viewport meta（必须包含）

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
```

> `viewport-fit=cover` 是 safe-area 适配的前提，不加这个 meta，`env(safe-area-inset-*)` 不生效。

### 表格移动端策略

桌面表格在移动端有三种处理方式，根据数据量选择：

1. **水平滚动**（列数少，数据重要）
```css
@media (max-width: 768px) {
  .table-wrapper { overflow-x: auto; -webkit-overflow-scrolling: touch; }
  .data-table { min-width: 600px; }
}
```

2. **卡片化**（列数多，每行可独立展示）
```css
@media (max-width: 768px) {
  .data-table thead { display: none; }
  .data-table, .data-table tbody, .data-table tr, .data-table td { display: block; width: 100%; }
  .data-table tr { margin-bottom: 12px; border: 1px solid var(--border); border-radius: var(--radius-md); padding: 8px; }
  .data-table td { display: flex; justify-content: space-between; padding: 8px 12px; border: none; }
  .data-table td::before { content: attr(data-label); color: var(--text-2); font-size: 12px; flex-shrink: 0; margin-right: 16px; }
}
```
```html
<!-- HTML 中 td 需要 data-label 属性 -->
<td data-label="名称">xxx</td>
<td data-label="状态">xxx</td>
```

3. **隐藏次要列**（列数多，部分列非关键）
```css
@media (max-width: 768px) {
  .data-table th.col-optional, .data-table td.col-optional { display: none; }
}
```

### 移动端验证清单

生成页面后，除了标准验证流程，额外检查以下移动端专项：

1. **viewport meta** — `viewport-fit=cover` 是否存在
2. **汉堡菜单** — Header 中是否有 `.hamburger` 元素和 `toggleMobileNav()` 函数
3. **断点完整性** — 是否同时包含 1024px、768px、480px 三个断点的 `@media` 规则
4. **单列回退** — 所有 `grid-template-columns: repeat(N, 1fr)` 是否都有对应的移动端单列回退
5. **Modal 全屏** — `.modal-box` 在 480px 断点下是否 `width: 100vw`
6. **Safe Area** — `.header` 和底部导航是否使用 `env(safe-area-inset-*)`
7. **触摸目标** — 可点击元素在移动端是否 >= 44px 高度
8. **无水平溢出** — `body { overflow-x: hidden }` 防止移动端水平滚动条

```bash
# 移动端专项验证脚本
python3 -c "
import re
with open('page.html','r') as f: html = f.read()

checks = []

# 1. viewport-fit=cover
checks.append(('viewport-fit=cover', 'viewport-fit=cover' in html))

# 2. 汉堡菜单
checks.append(('hamburger element', 'hamburger' in html and 'toggleMobileNav' in html))

# 3. 三档断点
for bp in ['1024', '768', '480']:
    checks.append((f'@media {bp}px', f'max-width:{bp}' in html or f'max-width: {bp}' in html))

# 4. grid 单列回退
checks.append(('grid 1fr mobile', 'grid-template-columns: 1fr' in html or 'grid-template-columns:1fr' in html))

# 5. Modal 全屏
checks.append(('modal 100vw', '100vw' in html))

# 6. safe-area
checks.append(('safe-area-inset', 'safe-area-inset' in html))

# 7. overflow-x hidden
checks.append(('overflow-x hidden', 'overflow-x' in html and 'hidden' in html))

for name, passed in checks:
    print(f'  {\"PASS\" if passed else \"FAIL\"} — {name}')
"
```

### 各风格的移动端差异

虽然上述骨架通用，但各风格在移动端有独特处理：

| 风格 | 移动端特殊处理 |
|---|---|
| 深色工业科技 | 背景光晕减少为 1 个，网格背景隐藏，backdrop-filter 降为 8px |
| 未来赛博 | 扫描线动画暂停，粒子数量减半，霓虹辉光阴影缩小 |
| 明亮科技 | 卡片间距从 16px 降至 12px，Bento Grid 直接单列 |
| 玻璃拟态 | backdrop-filter 降为 12px（性能），渐变光晕数量减为 1-2 个 |
| Apple 极简 | 留白保持，标题 28px，胶囊按钮全宽，滚动动画保留但缩短 |
| 明亮可爱 | 圆角从 32px 降至 20px，弹跳动画保留但更快（0.3s），Emoji 字号 36px |
| 新粗野主义 | 硬阴影从 4px 降至 3px，边框从 3px 降至 2px，保持视觉冲击 |
| 商务简约 | 间距压缩，无额外装饰变化，保持极简 |
| 数据仪表盘 | 侧边栏转底部 Tab 栏，图表高度降至 200px，表格水平滚动 |
| 国风雅致 | 水墨装饰隐藏（性能），留白保持，衬线字号 16px 最小 |

详细规则见各风格文件中的「移动端适配」章节。

---

## 组合配方：AI 产品风格

> 2025-2026 年 AI 产品最流行的组合：**玻璃拟态 + Bento Grid + 动效**
> 参考：OpenAI、Anthropic、Midjourney 首页风格

**配方组成**：
- 底色：深色渐变背景（深色工业风 `--bg-0` 或自定义深紫渐变）
- 布局：Bento Grid（本文件共享布局模式）
- 卡片：玻璃拟态半透明（加载 `styles/modern/glassmorphism.md`）
- 动效：fade-up 入场 + 悬浮微动 + 数字递增
- 点缀：渐变光效背景光晕

**快速构建步骤**：
1. 读取 `styles/modern/glassmorphism.md` 获取玻璃拟态 CSS 变量和卡片样式
2. 使用本文件的 Bento Grid 布局
3. 背景使用 `linear-gradient(135deg, #0F0C29, #302B63, #24243E)` 深紫渐变
4. 卡片使用 `rgba(255,255,255,0.08)` + `backdrop-filter: blur(20px)`
5. 添加 2-3 个彩色渐变光晕背景（紫、蓝、青）
6. Hero 区使用超大标题 + 渐变文字
7. 功能卡片内嵌图标 + 简短描述 + hover 光效

**关键 CSS 片段**：
```css
body { background: linear-gradient(135deg, #0F0C29, #302B63, #24243E); }
.hero-title {
  font-size: 64px; font-weight: 700; line-height: 1.1;
  background: linear-gradient(135deg, #fff 0%, rgba(255,255,255,0.6) 100%);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.bento-card {
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 20px;
  transition: all 0.4s var(--ease);
}
.bento-card:hover {
  background: rgba(255,255,255,0.12);
  border-color: rgba(255,255,255,0.20);
  transform: translateY(-4px);
  box-shadow: 0 20px 40px rgba(0,0,0,0.3);
}
```

---

## 风格对比速查表

| 维度 | 深色工业 | 未来赛博 | 明亮科技 | 玻璃拟态 | Apple极简 | 明亮可爱 | 新粗野 | 商务简约 | 数据仪表盘 | 国风雅致 |
|---|---|---|---|---|---|---|---|---|---|---|
| 底色 | #081018 | #0A0014 | #FFFFFF | 渐变 | #FFFFFF | #FFF8F4 | #FFE600 | #FAFAFA | #F8F9FB | #F5F0E8 |
| 主色 | #00C8D7 | #00FFFF | #0066FF | 白透明 | #1D1D1F | #FF6B6B | #000000 | #18181B | #2563EB | #8B2C2C |
| 圆角 | 8-16px | 4-8px | 8-16px | 16-24px | 12-20px | 12-32px | 0px | 6-12px | 6-10px | 6-14px |
| 阴影 | 中等+发光 | 强+荧光 | 轻柔 | 柔和+透光 | 极轻 | 柔和+色调 | 无(硬边框) | 极轻 | 中等 | 轻柔+暖色 |
| 动画 | 0.8s | 0.5s+扫描 | 0.6s | 0.5s+光效 | 0.8s+滚动 | 0.5s+弹跳 | 0.2s+硬切 | 0.4s | 0.3s | 1.0s |
| 字体 | 无衬线 | 等宽+无衬线 | 无衬线 | 无衬线 | SF Pro | 无衬线 | 粗无衬线 | 无衬线 | 无衬线 | 衬线为主 |
| 背景 | 网格+光晕 | 网格+粒子 | 微渐变 | 渐变+光效 | 纯净 | 渐变光斑 | 纯色 | 无装饰 | 灰白 | 水墨+纸纹 |
| Emoji | 不用 | 不用 | 不用 | 不用 | 不用 | 鼓励 | 不用 | 不用 | 不用 | 不用 |
| 留白 | 适中 | 适中 | 适中 | 适中 | 大量 | 适中 | 适中 | 适中 | 紧凑 | 大量 |
| blur | 12px | 4px | 20px | 20px | 0 | 16px | 无 | 无 | 8px | 12px |

---

## 快速构建 Checklist

1. **确定风格**：根据用途和用户偏好，用风格路由器选择风格
2. **读取风格文件**：加载对应 `styles/<category>/<style>.md` 获取完整设计体系
3. **初始化**：创建 `.html` 文件，写入 DOCTYPE、head、字体引用，viewport 必须包含 `viewport-fit=cover`
4. **CSS Variables**：复制对应风格的 `:root` 变量
5. **背景层**：按风格添加背景处理（网格/渐变/光斑/纸纹/无）
6. **Header**：按风格添加 Header 样式，**必须包含汉堡菜单组件**
7. **布局**：选择布局模式（标准 section / Bento Grid / Sidebar）
8. **组件**：复制共享组件 HTML 结构，按风格应用 CSS 变量
9. **JavaScript**：按模块顺序编写（Config → Utils → Data → Modal → History → Export → Init）
10. **响应式**：写入三档断点 @media 规则（1024px + 768px + 480px），实现网格降列、Header 汉堡菜单、Modal 全屏、Safe Area 适配、触摸目标 >= 44px
11. **验证**：执行完整验证流程（语法 + 括号 + 函数 + ID + onclick）+ 移动端专项验证（viewport-fit + 汉堡菜单 + 三档断点 + 单列回退 + Modal 全屏 + safe-area + overflow-x hidden）
12. **记录**：记录文件行数和字节数

---

## 参考实现

- **深色工业科技风**完整实现：`/home/bml/xdg_root/workspace/ai4s-platform.html`（3,306 行）
- 构建新风格页面时，以 `ai4s-platform.html` 为结构骨架，替换 `:root` CSS 变量和组件样式即可快速产出
- 该参考实现包含：Header 布局、Modal 系统、侧滑面板、下拉菜单、Toast、Tab 切换、表单、表格、CSV/Excel 导出、智能路由、历史系统、科研驾驶舱、Canvas 知识图谱、AI 助手、通知系统、用户菜单

---

## 3D Web 扩展技巧

当需要在纯 HTML/CSS/JS 中实现轻量 3D 效果时（不引入 Three.js）：

**CSS 3D Transform**
```css
.card-3d { transform-style: preserve-3d; transition: transform 0.6s var(--ease); }
.card-3d:hover { transform: rotateY(8deg) rotateX(4deg); }
```

**CSS Perspective**
```css
.perspective-container { perspective: 1000px; }
```

**Canvas 粒子系统**
```javascript
var particles = [];
function initParticles(canvas) {
  var ctx = canvas.getContext('2d');
  for (var i = 0; i < 80; i++) {
    particles.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      vx: (Math.random() - 0.5) * 0.5,
      vy: (Math.random() - 0.5) * 0.5,
      r: Math.random() * 2 + 0.5
    });
  }
  animateParticles(ctx, canvas);
}
```

适用于：产品展示卡片悬浮 3D 倾斜、背景粒子流动、视差滚动。

---

## 风格文件索引

| 文件路径 | 风格 | 状态 |
|---|---|---|
| `styles/dark/industrial-dark.md` | 深色工业科技风 | 已迁移 |
| `styles/dark/cyberpunk.md` | 未来赛博风 | 新增 |
| `styles/modern/bright-tech.md` | 明亮科技风 | 已迁移 |
| `styles/modern/glassmorphism.md` | 玻璃拟态风 | 新增 |
| `styles/modern/apple-minimal.md` | Apple 极简风 | 新增 |
| `styles/creative/bright-cute.md` | 明亮可爱风 | 已迁移 |
| `styles/creative/neobrutalism.md` | 新粗野主义 | 新增 |
| `styles/business/business-minimal.md` | 商务简约风 | 已迁移 |
| `styles/business/dashboard.md` | 数据仪表盘风 | 新增 |
| `styles/cultural/chinese-elegant.md` | 国风雅致风 | 已迁移 |
