# Frontend Page Builder

> 十种风格，一键构建前端页面。纯 HTML+CSS+JS 单文件，无需构建工具。
> 从润滑材料AI预测引擎项目沉淀，扩展为覆盖全部场景的通用前端构建体系。

## 它能做什么

一句话告诉 AI 你想要什么风格的页面，它就能输出一个完整可用的单页应用。

- **10 种设计风格** — 从深色工业科技到国风雅致，覆盖数据平台、AI 产品、SaaS、消费应用、管理后台、文化展示等全部场景
- **零依赖运行** — 纯 HTML+CSS+JS 单文件，双击即可在浏览器打开，不依赖 React/Vue/Next.js/构建工具
- **完整组件库** — Modal 系统、侧滑面板、下拉菜单、Toast、Tab 切换、表单、表格、CSV/Excel 导出、Canvas 图表、数字递增动画等开箱即用
- **验证流程内置** — 每次生成后自动执行 JS 语法校验、括号平衡、函数去重、HTML ID 完整性、onclick 绑定五项检查

---

## 怎么用

### 触发方式

在对话中直接描述你要的页面，AI 会自动识别风格关键词并触发本 Skill：

| 你说什么 | 触发的风格 |
|---|---|
| "做个深色科技风的监控大屏" | 深色工业科技风 |
| "来个赛博朋克风的游戏平台" | 未来赛博风 |
| "做一个清爽的 SaaS 后台" | 明亮科技风 |
| "做个毛玻璃效果的 AI 助手页面" | 玻璃拟态风 |
| "做一个 Apple 风格的产品官网" | Apple 极简风 |
| "做一个可爱风的打卡应用" | 明亮可爱风 |
| "做一个新粗野主义的独立产品页" | 新粗野主义 |
| "做一个简约商务的项目管理页" | 商务简约风 |
| "做一个数据仪表盘管理后台" | 数据仪表盘风 |
| "做一个国风水墨的文化展示页" | 国风雅致风 |

也可以直接说"做个页面"、"build a page"、"做个UI"，AI 会根据用途自动推断最合适的风格。

### 生成后的验证

每次生成页面后，AI 会自动执行五项验证：

1. **JS 语法校验** — `node --check` 零错误
2. **括号平衡** — `{}` / `()` / `[]` 各自配对相等
3. **函数去重** — 无重名函数
4. **HTML ID 完整性** — 所有 `id="xxx"` 在 JS 中被引用
5. **onclick 绑定** — 所有 `onclick="fn()"` 对应函数已定义

验证通过后你会看到行数和字节数报告。

### 打开生成的页面

生成的 `.html` 文件可以直接双击在浏览器打开，也可以通过 file-export 下载后查看。如果需要在局域网预览，可以让 AI 启动一个 HTTP 服务器。

---

## 十种风格一览

### Dark 深色系

**1. 深色工业科技风** `Industrial Dark`

- 配色：底色 `#081018`，主色青蓝 `#00C8D7`，辅色紫 `#7567FF`，警示红 `#C40018`
- 特征：网格背景 + 光晕浮动，中等阴影带发光效果，0.8s 过渡动画
- 适用：数据平台、科研工具、监控大屏、工业智能化系统
- 参考实现：`ai4s-platform.html`（3,306 行，润滑材料AI预测引擎）

**2. 未来赛博风** `Cyberpunk`

- 配色：底色 `#0A0014`，霓虹青 `#00FFFF`，霓虹品红 `#FF00FF`，荧光绿 `#00FF88`
- 特征：Orbitron + Share Tech Mono 字体，荧光辉光阴影，扫描线动画，粒子特效
- 适用：Web3、游戏平台、AI 实验室、元宇宙入口

### Modern 现代系

**3. 明亮科技风** `Bright Tech`

- 配色：底色 `#FFFFFF`，主色蓝 `#0066FF`，辅色紫 `#6B46FF`，成功绿 `#00B884`
- 特征：轻柔阴影，8-16px 圆角，0.6s 过渡，支持标准 Section 和 Bento Grid 布局
- 适用：SaaS 产品、管理后台、文档平台、Notion/Stripe 风格应用

**4. 玻璃拟态风** `Glassmorphism`

- 配色：渐变底色 `#6366F1` → `#A855F7` → `#EC4899`，半透明卡片 + `backdrop-filter: blur(20px)`
- 特征：16-24px 大圆角，柔和透光阴影，彩色光晕背景，0.5s 光效动画
- 适用：AI 产品、智能助手、创意工具、OpenAI/Anthropic 风格首页

**5. Apple 极简风** `Apple Minimal`

- 配色：底色 `#FFFFFF` / `#FBFBFD` / `#F5F5F7`，文字黑 `#1D1D1F`，链接蓝 `#0071E3`
- 特征：SF Pro 字体，大量留白，超大标题，980px 胶囊按钮，0.8s 滚动动画
- 适用：产品官网、品牌展示、高端 SaaS 落地页

### Creative 创意系

**6. 明亮可爱风** `Bright Cute`

- 配色：底色 `#FFF8F4`，主色珊瑚红 `#FF6B6B`，辅色薄荷绿 `#4ECDC4`，点缀黄 `#FFD93D`
- 特征：12-32px 大圆角，弹跳/摇摆动画，鼓励使用 Emoji，Duolingo/飞书风格
- 适用：教育产品、消费应用、引导页、习惯打卡
- 参考实现：`cute-habit-tracker.html`（844 行，习惯打卡应用）

**7. 新粗野主义** `Neobrutalism`

- 配色：底色亮黄 `#FFE600`，边框纯黑 `#000000`，点缀品红 `#FF3366`，青绿 `#4ECDC4`
- 特征：3px 粗黑边框，硬阴影 `4px 4px 0px #000`（无模糊），0-8px 小圆角，0.2s 硬切动画
- 适用：创意品牌、独立产品、开发者工具、Gumroad 风格着陆页

### Business 商务系

**8. 商务简约风** `Business Minimal`

- 配色：底色 `#FAFAFA`，文字 `#18181B`，点缀蓝 `#3B82F6`，极致克制无装饰
- 特征：6-12px 圆角，极轻阴影，0.4s 克制动画，Linear/Vercel 风格
- 适用：企业内部系统、项目管理、API 平台、开发者文档

**9. 数据仪表盘风** `Dashboard`

- 配色：底色 `#F8F9FB`，侧边栏深灰 `#1E293B`，主色蓝 `#2563EB`，辅色紫 `#7C3AED`
- 特征：侧边栏 + 内容区布局，6-10px 圆角，表格 + 图表组件，tabular-nums 数字
- 适用：管理后台、ERP/CRM、数据看板、运营报表

### Cultural 文化系

**10. 国风雅致风** `Chinese Elegant`

- 配色：宣纸白 `#F5F0E8`，朱砂红 `#8B2C2C`，青黛蓝 `#2C5F7C`，苍翠绿 `#5B7A3A`，赭石金 `#8B6914`
- 特征：Noto Serif SC 衬线字体，水墨/印章装饰，6-14px 圆角，1.0s 缓慢动画，大量留白
- 适用：文化展示、博物馆数字馆、传统工艺、茶道/书画展示

---

## 视觉画廊

打开 `showcase.html` 可以在一个页面内浏览全部 10 种风格的视觉预览，包括配色方案、迷你 UI 组件预览和元数据标签。

```bash
# 直接打开
open showcase.html

# 或通过 HTTP 服务器预览
python3 -m http.server 8848 --directory .
# 然后访问 http://localhost:8848/showcase.html
```

画廊页面功能：
- 每种风格一张卡片，包含图标、名称、分类标签
- 6 色色板预览（鼠标悬停显示色值和变量名）
- 迷你 UI 预览（卡片 + 按钮的真实渲染效果）
- 元数据标签（圆角、阴影、字体、动画、适用场景）
- 滚动入场动画（IntersectionObserver fade-up）

---

## 风格对比速查

| 维度 | 深色工业 | 未来赛博 | 明亮科技 | 玻璃拟态 | Apple极简 | 明亮可爱 | 新粗野 | 商务简约 | 数据仪表盘 | 国风雅致 |
|---|---|---|---|---|---|---|---|---|---|---|
| 底色 | #081018 | #0A0014 | #FFFFFF | 渐变 | #FFFFFF | #FFF8F4 | #FFE600 | #FAFAFA | #F8F9FB | #F5F0E8 |
| 主色 | #00C8D7 | #00FFFF | #0066FF | 白透明 | #1D1D1F | #FF6B6B | #000000 | #18181B | #2563EB | #8B2C2C |
| 圆角 | 8-16px | 4-8px | 8-16px | 16-24px | 12-20px | 12-32px | 0px | 6-12px | 6-10px | 6-14px |
| 阴影 | 中等+发光 | 强+荧光 | 轻柔 | 柔和+透光 | 极轻 | 柔和+色调 | 硬边框 | 极轻 | 中等 | 轻柔+暖色 |
| 动画 | 0.8s | 0.5s+扫描 | 0.6s | 0.5s+光效 | 0.8s+滚动 | 0.5s+弹跳 | 0.2s+硬切 | 0.4s | 0.3s | 1.0s |
| 字体 | 无衬线 | 等宽+无衬线 | 无衬线 | 无衬线 | SF Pro | 无衬线 | 粗无衬线 | 无衬线 | 无衬线 | 衬线为主 |
| 背景 | 网格+光晕 | 网格+粒子 | 微渐变 | 渐变+光效 | 纯净 | 渐变光斑 | 纯色 | 无装饰 | 灰白 | 水墨+纸纹 |
| 留白 | 适中 | 适中 | 适中 | 适中 | 大量 | 适中 | 适中 | 适中 | 紧凑 | 大量 |

---

## 工程规范

### 单文件架构

所有 HTML、CSS、JavaScript 写在一个 `.html` 文件中：

```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <style>
    /* 1. CSS Variables  2. Reset & Base  3. Background */
    /* 4. Header         5. Sections      6. Components   */
    /* 7. Forms          8. Responsive                     */
  </style>
</head>
<body>
  <!-- Background → Header → Main → Modals/Panels → Footer -->
  <script>
    /* 1. Config  2. Utils  3. Data    4. Modal   5. History */
    /* 6. Export  7. Detail 8. Dashboard 9. Init             */
  </script>
</body>
</html>
```

### 代码风格

- 使用 `var` 而非 `let` / `const`
- 函数声明使用 `function name(){}`
- 字符串单引号，HTML 拼接用 `+=`
- 使用 `forEach` 而非 `for...of`
- 不使用 ES Modules / TypeScript

### 外部依赖

- Google Fonts — 字体
- SmilesDrawer — 分子结构渲染（仅科研场景）
- 原则：外部依赖最多 2-3 个，CDN 必须锁版本号，不使用 jQuery / Bootstrap / Tailwind

### 内置组件

| 组件 | 说明 |
|---|---|
| Modal 系统 | 弹窗 + 表单 + Loading 进度条 + 结果展示 |
| 侧滑面板 | 右侧滑出，420px 宽 |
| 下拉菜单 | 顶部下拉，380px 宽 |
| Toast | 右上角通知，3 秒自动消失 |
| Tab 切换 | 胶囊式标签页 |
| 表单组件 | 输入框 + 标签芯片 + 下拉选择 |
| 数据表格 | 可排序、可点击行 |
| CSV/Excel 导出 | 前端生成文件下载 |
| Canvas 图表 | 柱状图、趋势图、知识图谱 |
| 数字递增动画 | requestAnimationFrame + easeOutCubic |

### 布局模式

- **标准 Section** — 逐段垂直排列，适合大多数场景
- **Bento Grid** — 模块化网格，信息密度高，适合功能展示页
- **Sidebar 布局** — 侧边栏 + 内容区，适合管理后台

---

## 组合配方：AI 产品风格

2025-2026 年 AI 产品最流行的组合：**玻璃拟态 + Bento Grid + 动效**。

参考 OpenAI、Anthropic、Midjourney 首页风格。

快速构建步骤：

1. 加载 `styles/modern/glassmorphism.md` 获取玻璃拟态 CSS 变量
2. 使用 Bento Grid 布局
3. 背景使用深紫渐变 `linear-gradient(135deg, #0F0C29, #302B63, #24243E)`
4. 卡片使用 `rgba(255,255,255,0.08)` + `backdrop-filter: blur(20px)`
5. 添加 2-3 个彩色渐变光晕背景
6. Hero 区使用超大标题 + 渐变文字
7. 功能卡片内嵌图标 + 简短描述 + hover 光效

---

## 示例文件

| 文件 | 风格 | 行数 | 说明 |
|---|---|---|---|
| `ai4s-platform.html` | 深色工业科技风 | 3,306 | 润滑材料AI预测引擎，含预测表单、历史记录、科研驾驶舱、知识图谱、AI 助手 |
| `cute-habit-tracker.html` | 明亮可爱风 | 844 | 习惯打卡应用，含习惯管理、连续天数、打卡动画、统计面板 |
| `showcase.html` | 深色工业科技风（画廊页） | 660 | 十风格视觉画廊，展示全部 10 种风格的配色和迷你 UI 预览 |

---

## 目录结构

```
frontend-page-builder/
├── SKILL.md                          # 主索引：风格路由器 + 共享规范 + 组件库
├── README.md                         # 本文件
├── showcase.html                     # 视觉画廊页面
├── styles/
│   ├── dark/
│   │   ├── industrial-dark.md        # 深色工业科技风
│   │   └── cyberpunk.md              # 未来赛博风
│   ├── modern/
│   │   ├── bright-tech.md            # 明亮科技风
│   │   ├── glassmorphism.md          # 玻璃拟态风
│   │   └── apple-minimal.md          # Apple 极简风
│   ├── creative/
│   │   ├── bright-cute.md            # 明亮可爱风
│   │   └── neobrutalism.md           # 新粗野主义
│   ├── business/
│   │   ├── business-minimal.md       # 商务简约风
│   │   └── dashboard.md              # 数据仪表盘风
│   └── cultural/
│       └── chinese-elegant.md        # 国风雅致风
```

---

## 快速构建 Checklist

1. **确定风格** — 根据用途和用户偏好，用风格路由器选择风格
2. **读取风格文件** — 加载对应 `styles/<category>/<style>.md` 获取完整设计体系
3. **初始化** — 创建 `.html` 文件，写入 DOCTYPE、head、字体引用
4. **CSS Variables** — 复制对应风格的 `:root` 变量
5. **背景层** — 按风格添加背景处理（网格/渐变/光斑/纸纹/无）
6. **Header** — 按风格添加 Header 样式
7. **布局** — 选择布局模式（标准 section / Bento Grid / Sidebar）
8. **组件** — 复制共享组件 HTML 结构，按风格应用 CSS 变量
9. **JavaScript** — 按模块顺序编写（Config → Utils → Data → Modal → History → Export → Init）
10. **验证** — 执行完整验证流程（语法 + 括号 + 函数 + ID + onclick）
11. **记录** — 记录文件行数和字节数
