# 数据仪表盘风（Dashboard）

> 参考：Vercel Dashboard、Stripe Dashboard、Linear、Notion Database、Grafana
> 适用：管理后台、ERP/CRM 系统、数据看板、监控系统、运营管理平台

## 配色体系

```css
:root {
  /* 底色层 — 浅灰体系 */
  --bg-0: #F8F9FB;          /* 全局背景，极浅灰 */
  --bg-1: #FFFFFF;          /* 卡片/面板白 */
  --bg-2: #F1F3F5;          /* 悬浮/嵌套灰 */
  --bg-3: #E9ECEF;          /* 边缘/分隔 */

  /* 侧边栏深色 */
  --sidebar-bg: #1E293B;    /* 深蓝灰侧边栏 */
  --sidebar-hover: #334155;
  --sidebar-active: #2563EB;

  /* 主色 */
  --accent: #2563EB;         /* 蓝色主交互 */
  --accent-glow: rgba(37,99,235,0.10);
  --accent-2: #7C3AED;       /* 紫色辅助 */
  --accent-3: #059669;       /* 绿色点缀 */

  /* 语义色 */
  --success: #10B981;
  --warning: #F59E0B;
  --danger: #EF4444;
  --info: #3B82F6;

  /* 文字层级 */
  --text-0: #0F172A;        /* 标题，极深蓝灰 */
  --text-1: #334155;        /* 正文 */
  --text-2: #64748B;        /* 次要 */
  --text-3: #94A3B8;        /* 标签/占位 */

  /* 边框 */
  --border: #E2E8F0;
  --border-strong: #CBD5E1;

  /* 阴影 — 轻柔 */
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.04);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.06);
  --shadow-lg: 0 8px 24px rgba(0,0,0,0.08);

  /* 圆角 — 小到中等 */
  --radius-sm: 6px; --radius-md: 8px; --radius-lg: 10px; --radius-xl: 12px;

  /* 缓动 */
  --ease: cubic-bezier(0.4,0,0.2,1);
  --ease-smooth: cubic-bezier(0.25,0.1,0.25,1);

  --header-h: 56px;
  --sidebar-w: 240px;
  --sidebar-w-collapsed: 64px;
  --font-cn: "HarmonyOS Sans","Noto Sans SC","PingFang SC",sans-serif;
  --font-en: "Inter",-apple-system,sans-serif;
  --font-mono: "JetBrains Mono","Courier New",monospace;
}
```

**设计原则**
- 左侧固定侧边栏 + 右侧内容区是标准布局，侧边栏深色与内容区浅色形成对比
- 信息密度高但有序：使用网格布局排列数据卡片，每张卡片有明确的标题、数值、趋势
- 表格是核心组件：斑马纹、可排序、可分页、行 hover 高亮
- 图表使用 CSS 柱状图/折线图或 Canvas 绘制（无需引入 Chart.js，保持单文件架构）
- 状态指示器使用色点 + 文字（绿色=正常，黄色=警告，红色=异常）
- 操作按钮小而精，不抢数据展示的视觉焦点

## 布局骨架

```css
.layout {
  display: flex; min-height: 100vh;
}

/* 侧边栏 */
.sidebar {
  width: var(--sidebar-w); background: var(--sidebar-bg);
  position: fixed; top: 0; left: 0; bottom: 0; z-index: 900;
  display: flex; flex-direction: column; padding: 16px 0;
  transition: width 0.3s var(--ease);
  overflow-y: auto;
}
.sidebar.collapsed { width: var(--sidebar-w-collapsed); }

/* 主内容区 */
.main {
  flex: 1; margin-left: var(--sidebar-w);
  display: flex; flex-direction: column; min-height: 100vh;
  transition: margin-left 0.3s var(--ease);
}
.main.sidebar-collapsed { margin-left: var(--sidebar-w-collapsed); }

/* 顶栏 */
.topbar {
  height: var(--header-h); background: var(--bg-1);
  border-bottom: 1px solid var(--border);
  display: flex; align-items: center; padding: 0 24px;
  position: sticky; top: 0; z-index: 800;
}

/* 内容区 */
.content { padding: 24px; flex: 1; }
```

**HTML 结构**
```html
<div class="layout">
  <aside class="sidebar" id="sidebar">
    <!-- 导航项 -->
  </aside>
  <div class="main" id="main">
    <header class="topbar">
      <!-- 顶栏内容 -->
    </header>
    <main class="content">
      <!-- 数据卡片、表格、图表 -->
    </main>
  </div>
</div>
```

## 侧边栏导航

```css
.sidebar-logo {
  padding: 0 20px 16px; color: #FFFFFF; font-size: 18px; font-weight: 700;
  border-bottom: 1px solid rgba(255,255,255,0.08); margin-bottom: 8px;
}
.nav-group { padding: 8px 12px; }
.nav-group-title {
  font-size: 11px; color: #64748B; text-transform: uppercase;
  letter-spacing: 0.5px; padding: 8px 8px 4px;
}
.nav-item {
  display: flex; align-items: center; gap: 10px;
  padding: 8px 12px; color: #94A3B8; font-size: 14px;
  border-radius: var(--radius-sm); cursor: pointer;
  transition: all 0.2s var(--ease); text-decoration: none;
}
.nav-item:hover { background: var(--sidebar-hover); color: #E2E8F0; }
.nav-item.active { background: var(--sidebar-active); color: #FFFFFF; }
.nav-item .nav-icon { width: 18px; height: 18px; flex-shrink: 0; }
.nav-item .nav-badge {
  margin-left: auto; font-size: 11px; padding: 1px 7px;
  background: var(--danger); color: #FFFFFF; border-radius: 999px;
}
```

## 数据卡片

```css
/* 统计卡片网格 */
.stat-grid {
  display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 16px; margin-bottom: 24px;
}
.stat-card {
  background: var(--bg-1); border: 1px solid var(--border);
  border-radius: var(--radius-md); padding: 20px;
  transition: all 0.2s var(--ease);
}
.stat-card:hover { box-shadow: var(--shadow-md); }
.stat-label { font-size: 13px; color: var(--text-2); margin-bottom: 8px; }
.stat-value {
  font-size: 28px; font-weight: 700; color: var(--text-0);
  font-family: var(--font-en); line-height: 1.2;
}
.stat-trend { font-size: 13px; margin-top: 8px; display: flex; align-items: center; gap: 4px; }
.stat-trend.up { color: var(--success); }
.stat-trend.down { color: var(--danger); }
.stat-trend.flat { color: var(--text-3); }
```

## 表格

```css
.table-wrap {
  background: var(--bg-1); border: 1px solid var(--border);
  border-radius: var(--radius-md); overflow: hidden;
}
.data-table { width: 100%; border-collapse: collapse; font-size: 14px; }
.data-table thead { background: var(--bg-2); }
.data-table th {
  padding: 12px 16px; text-align: left; font-weight: 600;
  color: var(--text-2); font-size: 13px;
  border-bottom: 1px solid var(--border); white-space: nowrap;
  cursor: pointer; user-select: none;
}
.data-table th:hover { color: var(--text-0); }
.data-table td {
  padding: 12px 16px; color: var(--text-1);
  border-bottom: 1px solid var(--border);
}
.data-table tbody tr { transition: background 0.15s; }
.data-table tbody tr:hover { background: var(--bg-2); }
.data-table tbody tr:nth-child(even) { background: rgba(241,243,245,0.50); }
.data-table tbody tr:nth-child(even):hover { background: var(--bg-2); }
.data-table .col-num { font-family: var(--font-mono); text-align: right; }

/* 分页 */
.pagination {
  display: flex; align-items: center; justify-content: space-between;
  padding: 12px 16px; border-top: 1px solid var(--border);
}
.page-info { font-size: 13px; color: var(--text-2); }
.page-btns { display: flex; gap: 4px; }
.page-btn {
  padding: 6px 12px; border: 1px solid var(--border); background: var(--bg-1);
  border-radius: var(--radius-sm); font-size: 13px; cursor: pointer;
  color: var(--text-1); transition: all 0.2s;
}
.page-btn:hover { border-color: var(--accent); color: var(--accent); }
.page-btn.active { background: var(--accent); color: #FFFFFF; border-color: var(--accent); }
.page-btn:disabled { opacity: 0.4; cursor: not-allowed; }
```

## CSS 图表（无依赖）

```css
/* 柱状图 */
.bar-chart { display: flex; align-items: flex-end; gap: 8px; height: 200px; padding: 16px 0; }
.bar-item { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 6px; }
.bar {
  width: 100%; max-width: 40px; background: linear-gradient(180deg, var(--accent), var(--accent-2));
  border-radius: var(--radius-sm) var(--radius-sm) 0 0;
  transition: all 0.3s var(--ease); min-height: 4px;
  position: relative;
}
.bar:hover { opacity: 0.85; }
.bar-label { font-size: 11px; color: var(--text-3); }

/* 趋势线 — SVG 内联 */
.trend-chart { width: 100%; height: 120px; }
.trend-chart path { fill: none; stroke: var(--accent); stroke-width: 2; }
.trend-chart .area { fill: var(--accent-glow); stroke: none; }

/* 环形进度 — CSS conic-gradient */
.ring-progress {
  width: 80px; height: 80px; border-radius: 50%;
  background: conic-gradient(var(--accent) var(--p, 0%), var(--bg-3) 0%);
  display: flex; align-items: center; justify-content: center;
}
.ring-progress::after {
  content: ''; width: 60px; height: 60px; border-radius: 50%;
  background: var(--bg-1); position: absolute;
}
.ring-progress span { position: relative; z-index: 1; font-size: 16px; font-weight: 700; color: var(--text-0); }
```

## 状态指示器

```css
.status { display: inline-flex; align-items: center; gap: 6px; font-size: 13px; }
.status-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
.status-ok .status-dot { background: var(--success); box-shadow: 0 0 0 3px rgba(16,185,129,0.15); }
.status-warn .status-dot { background: var(--warning); box-shadow: 0 0 0 3px rgba(245,158,11,0.15); }
.status-err .status-dot { background: var(--danger); box-shadow: 0 0 0 3px rgba(239,68,68,0.15); }
```

## 按钮

```css
.btn-primary {
  background: var(--accent); color: #FFFFFF;
  padding: 8px 20px; border: none; border-radius: var(--radius-sm);
  font-size: 14px; font-weight: 500; cursor: pointer;
  transition: all 0.2s var(--ease);
}
.btn-primary:hover { background: #1D4ED8; }
.btn-primary:active { transform: scale(0.98); }

.btn-ghost {
  background: transparent; color: var(--text-1);
  border: 1px solid var(--border); padding: 8px 20px;
  border-radius: var(--radius-sm); font-size: 14px; cursor: pointer;
  transition: all 0.2s var(--ease);
}
.btn-ghost:hover { background: var(--bg-2); border-color: var(--border-strong); }

/* 图标按钮 */
.btn-icon {
  width: 32px; height: 32px; display: flex; align-items: center; justify-content: center;
  border: 1px solid var(--border); background: var(--bg-1); border-radius: var(--radius-sm);
  cursor: pointer; transition: all 0.2s;
}
.btn-icon:hover { background: var(--bg-2); }
```

## 表单

```css
.input, .select, .textarea {
  background: var(--bg-1); border: 1px solid var(--border);
  color: var(--text-0); padding: 8px 12px;
  border-radius: var(--radius-sm); font-size: 14px;
  transition: all 0.2s var(--ease);
}
.input:focus, .select:focus, .textarea:focus {
  outline: none; border-color: var(--accent);
  box-shadow: 0 0 0 3px var(--accent-glow);
}
.input::placeholder { color: var(--text-3); }

/* 搜索框 — 带图标 */
.search-box {
  display: flex; align-items: center; gap: 8px;
  background: var(--bg-2); border: 1px solid var(--border);
  border-radius: var(--radius-sm); padding: 0 12px;
}
.search-box input { background: none; border: none; outline: none; padding: 8px 0; font-size: 14px; flex: 1; }
```

## Modal 样式

```css
.modal-overlay { background: rgba(15,23,42,0.40); }
.modal-box {
  background: var(--bg-1); border: 1px solid var(--border);
  border-radius: var(--radius-lg); box-shadow: var(--shadow-lg);
}
.modal-head { border-bottom: 1px solid var(--border); padding: 16px 20px; }
.modal-foot { border-top: 1px solid var(--border); padding: 16px 20px; }
```

## 特色动画

```css
/* 数字滚动 — 数据更新时 */
@keyframes numRoll {
  0% { opacity: 0.5; transform: translateY(-4px); }
  100% { opacity: 1; transform: translateY(0); }
}
.num-update { animation: numRoll 0.4s var(--ease); }

/* 柱状图入场 — 逐根弹起 */
@keyframes barRise {
  0% { height: 0; opacity: 0; }
  100% { opacity: 1; }
}

/* 卡片入场 — 列表错峰 */
@keyframes cardSlideIn {
  0% { opacity: 0; transform: translateY(12px); }
  100% { opacity: 1; transform: translateY(0); }
}
.card-in { animation: cardSlideIn 0.3s var(--ease) forwards; }
.card-in:nth-child(1) { animation-delay: 0ms; }
.card-in:nth-child(2) { animation-delay: 60ms; }
.card-in:nth-child(3) { animation-delay: 120ms; }
.card-in:nth-child(4) { animation-delay: 180ms; }
.card-in:nth-child(5) { animation-delay: 240ms; }
.card-in:nth-child(6) { animation-delay: 300ms; }
```

## 适用场景与禁忌

- 适合：管理后台、ERP/CRM 系统、数据看板、监控系统、运营管理平台、内容管理系统
- 禁忌：不可使用大圆角（>12px，数据界面需要精确感）；不可使用鲜艳的装饰色（保持专业克制）；不可使用过重的阴影（阴影模糊不超过 12px）；不可使用装饰性动画（所有动画必须功能性，如数据更新反馈）；不可省略侧边栏（侧边栏是仪表盘的核心导航模式）；信息密度不可过低（每屏应展示足够数据，留白不是此风格的目标）
