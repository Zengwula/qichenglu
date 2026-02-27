<div align="center">

# 🚀 启程录

### 离开轨道，步入属于你的旷野

**专为求职者打造的全流程投递追踪工具**

轻量 · 美观 · 单文件部署 · 云端同步

[![GitHub Pages](https://img.shields.io/badge/Demo-GitHub%20Pages-blue?style=flat-square&logo=github)](https://your-username.github.io/qichenglu)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Made with](https://img.shields.io/badge/Made%20with-HTML%20%2B%20JS-orange?style=flat-square)](#技术栈)

</div>

---

## ✨ 这是什么？

**启程录**是一个纯前端的求职投递管理工具，帮你追踪从「待投递」到「拿到 Offer」的完整流程。

不需要安装任何东西，不需要下载 App——打开网页就能用。一个 HTML 文件，包含了你求职路上需要的一切。

> 每一次投递，都是一次新的启程。

---

## 🎯 核心功能

### 📋 流水线看板

纵向流水线布局，一眼看清所有投递的进度。从「待投递」到「Offer」，每个阶段一目了然。支持展开/折叠，点击顶部状态标签即可快速筛选。

### ⏱️ 智能时间线

每条投递都有详细的时间线视图，记录投递日期、每轮面试的时间和结果。**面试结果会自动推进投递状态**——一面通过后自动变为二面状态，无需手动切换。

### 📝 面经本

所有面试记录和面经笔记自动汇总，支持搜索和直接编辑，方便复盘和积累。

### 📅 面试日历

月历形式展示所有面试安排，再也不会忘记面试时间。

### 📊 数据统计

丰富的可视化图表：战绩摘要、面试转化漏斗、企业类型分布、城市分布、时间热力图、公司进度追踪表……用数据驱动你的求职策略。

### 🤖 AI 助手

内置三大 AI 功能，接入 DeepSeek / 通义千问：

| 功能 | 说明 |
|------|------|
| **弱点雷达** | AI Agent 多步分析你的所有面经，找出知识盲区和薄弱点 |
| **面试复盘** | 选择一条面经，AI 分析表现并给出改进建议 |
| **智能周报** | 基于全部数据生成本周求职进度总结和行动建议 |

### 🏆 成就系统

投递之路、面试达人、笔耕不辍、收割 Offer……解锁成就徽章，给求职旅程加点乐趣。

### ☁️ 云端同步

登录后数据自动同步到云端，换设备无缝衔接。基于 Supabase 构建，安全可靠。

---

## 🛠️ 技术栈

```
整个应用 = 1 个 HTML 文件，零依赖构建
```

| 技术 | 用途 |
|------|------|
| **原生 HTML / CSS / JS** | 全部界面和逻辑 |
| **Supabase** | 用户认证 + 数据云同步 |
| **Lucide Icons** | 图标库 |
| **DeepSeek / 通义千问 API** | AI 助手功能 |

没有 React，没有 Vue，没有 Webpack，没有 node_modules。打开就能跑。

---

## 🚀 部署方式

### 方式一：GitHub Pages（推荐）

1. Fork 本仓库
2. 在仓库 Settings → Pages 中开启 GitHub Pages
3. 访问 `https://你的用户名.github.io/仓库名`

### 方式二：任意静态托管

把 `index.html` 丢到任何静态文件服务器上即可，包括但不限于：

- Vercel / Netlify / Cloudflare Pages
- Nginx / Apache
- 甚至直接双击在本地打开

---

## ⚙️ 配置说明

### Supabase 数据库

应用使用 Supabase 进行用户认证和数据同步。如果你想自建实例：

1. 在 [Supabase](https://supabase.com) 创建项目
2. 创建以下数据表：

```sql
-- 投递记录表
create table entries (
  id text primary key,
  user_id uuid references auth.users(id),
  data jsonb,
  updated_at bigint
);

-- 用户设置表
create table user_settings (
  user_id uuid primary key references auth.users(id),
  settings jsonb,
  updated_at timestamptz default now()
);

-- RLS 策略
alter table entries enable row level security;
alter table user_settings enable row level security;

create policy "Users can manage own entries"
  on entries for all using (auth.uid() = user_id);

create policy "Users can manage own settings"
  on user_settings for all using (auth.uid() = user_id);
```

3. 将 `index.html` 中的 `SUPABASE_URL` 和 `SUPABASE_KEY` 替换为你的项目凭证

### 用户管理

应用不开放注册，用户由管理员在 Supabase 后台手动添加：

**Supabase Dashboard → Authentication → Users → Add User**

### AI 功能

用户需要在应用内「设置」中自行配置 AI 服务商和 API Key：

- **DeepSeek**：在 [platform.deepseek.com](https://platform.deepseek.com) 获取 Key
- **通义千问**：在 [阿里云百炼](https://bailian.console.aliyun.com) 获取 Key

Key 仅存储在用户浏览器本地（登录后可同步到云端加密存储）。

---

## 📱 兼容性

- ✅ iOS Safari（支持 PWA 添加到主屏幕）
- ✅ Android Chrome
- ✅ 桌面端各主流浏览器
- ✅ 适配 iPhone 安全区域（刘海 / 灵动岛）

---

## 📂 项目结构

```
.
└── index.html    ← 就这一个文件，没了
```

对，真的就一个文件。

---

## 🗺️ Roadmap

- [ ] 多端实时同步（WebSocket）
- [ ] 投递数据导入（从牛客/BOSS直聘）
- [ ] 面试提醒（邮件/推送）
- [ ] 团队协作模式
- [ ] 更多 AI 能力（模拟面试、简历优化）

---

## 📄 License

[MIT](LICENSE) © 2025

---

<div align="center">

**如果觉得有用，欢迎 ⭐ Star**

*求职不易，愿每一次启程都不被辜负。*

</div>
