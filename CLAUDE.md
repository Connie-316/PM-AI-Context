# [数智聚模-启泰物料集采商城] - 产品知识库

## 目录结构

| 目录 | 定位 |
|------|------|
| context/ | 产品知识库（已上线功能、架构、团队） |
| workspace/ | 工作区（PRD、需求、讨论） |
| drafts/ | 草稿区（临时想法、方案探索） |
| templates/ | 文档模板库（PRD/需求分析/会议纪要/上线检查清单） |
| .claude/commands/ | Skills（AI 标准作业程序） |

## 快速入口（你只需要看这两个）

| 文件 | 什么时候看 |
|------|---------|
| [START_HERE.md](START_HERE.md) | 第一次用 / 忘了怎么用 |
| [SKILL_GUIDE.md](SKILL_GUIDE.md) | 忘记了触发词 / 不知道用哪个 |

## Skill 优先规则

收到任务后，先扫描 .claude/commands/ 是否有对应 Skill。
有则必须调用该 Skill，不直接回答。

---

## Skill 索引

### PRD 与需求分析

| Skill | 触发词 | 使用场景 |
|-------|--------|---------|
| `requirements-analysis.md` | "需求分析"、"分析需求" | PRD 撰写前的需求调研与确认 |
| `full-prd.md` | "完整PRD"、"正式PRD" | 必须先完成需求分析，再写完整 PRD |
| `prd-write.md` | "快速PRD"、"帮我写个PRD" | 单个功能直接写，快速输出 |
| `dev-handoff.md` | "输出研发文档"、"写接口需求" | PRD完成后开发前，输出研发可读文档 |

### 文档管理

| Skill | 触发词 | 使用场景 |
|-------|--------|---------|
| `doc-review.md` | "检查文档"、"审阅PRD" | 文档修改后审查，自动触发 |
| `doc-version.md` | "查版本"、"看历史"、"回退" | 文档版本管理，每次修改自动记录 |
| `doc-archive.md` | "归档"、"上线了" | 功能上线后归档到 context |

### 周期工作

| Skill | 触发词 | 使用场景 |
|-------|--------|---------|
| `monthly-plan.md` | "月度规划"、"关键任务规划" | 每月25号规划下月关键任务（15号/31号上线） |
| `weekly-review.md` | "周复盘"、"本周总结" | 每周五复盘，发现问题并改进 |
| `tapd-sync.md` | "TAPD对齐"、"迭代乱了"、"同步TAPD" | 同步TAPD迭代版本，记录组长跳过的需求 |

### 工作追踪

| 文档 | 用途 |
|------|------|
| `workspace/需求池管理.md` | 所有需求进来时的统一登记（来源/优先级/状态） |
| `workspace/迭代规划对照表_YYYY-MM.md` | TAPD迭代版本的对照表（每月一个） |

### UI 规范

| Skill | 触发词 | 主题色 | 使用场景 |
|-------|--------|--------|---------|
| `ui-spec-miniprogram.md` | "小程序UI"、"商城UI" | #3370FF 蓝 | 小程序端 |
| `ui-spec-portal.md` | "门户端UI"、"官网UI" | #1664FF 蓝 | 门户商城PC/H5端 |
| `ui-spec-merchant.md` | "商家端UI" | #1664FF 蓝 | 商家端后台 |
| `ui-spec-supplier.md` | "供应商端UI" | #1664FF 蓝 | 供应商端后台 |
| `ui-spec-platform.md` | "平台端UI"、"运营后台" | #1664FF 蓝 | 平台运营后台 |

### 工具类

| Skill | 触发词 | 使用场景 |
|-------|--------|---------|
| `git-push.md` | "推送"、"提交"、"推送到GitHub" | GitHub 推送 |
| `ui-demo-preview.html` | "UI规范预览"、"可视化demo" | 各端 UI 规范浏览器预览 |

### Demo 文件

| 文件 | 用途 |
|------|------|
| `ui-demo-preview.html` | 各端 UI 规范可视化预览 |
| `ui-demo-print-label-full.html` | 打印标签+打单发货+发货记录完整页面交互 |

---

## 核心路由

- 问"现在产品是什么样的" → 读 context/
- 问"最近在做什么" → 读 workspace/
- 记录临时想法 → 放 drafts/
- 新需求进来 → 登记到 workspace/需求池管理.md
- TAPD迭代版本有变化 → 用 tapd-sync 同步更新迭代规划对照表
- 问 UI 规范 → 按端加载对应 skill
- 文档修改后 → 自动调用 doc-review + doc-version
- 功能上线后 → 自动提醒归档（doc-archive）
- 每月25号 → 自动提醒做月度规划（monthly-plan）
- 每周五 → 自动提醒做周复盘（weekly-review）
- PRD完成后 → 输出研发文档（dev-handoff）
- 文档确认后 → 自动推送 GitHub（git-push，无需用户说）

---

## 工作流总览

```
新需求进入
    ↓
登记到 需求池管理.md（来源/优先级/状态）
    ↓
需求评审（需求分析 Skill）
    ↓
写 PRD（prd-write / full-prd）
    ↓
doc-version 保存版本（自动）
    ↓
doc-review 审查（自动）
    ↓
确认后 → dev-handoff 输出研发文档
    ↓
研发签字确认
    ↓
进入开发阶段
    ↓
测试阶段 → PM 验收业务逻辑
    ↓
上线前 → 上线检查清单
    ↓
上线后 → doc-archive 归档
         → weekly-review 周复盘
         → git-push 推送
    ↓
每月25号 → monthly-plan 规划下月关键任务
```

---

## 颜色主题速查

| 端 | 主题色 | 辅助色 |
|----|--------|-------|
| 小程序端 | #3370FF 蓝 | 价格 #F5222C / 促销 #FF6B35 |
| 门户商城端 | #1664FF 蓝 | 金刚区橙 #FF7700 |
| 商家端 | #1664FF 蓝 | 统计卡橙 #FF7700 |
| 供应商端 | #1664FF 蓝 | 统计卡橙 #FF7700 |
| 平台端 | #1664FF 蓝 | 统计卡橙 #FF7700 |

**PC 后台通用规范：** 顶部导航/侧边菜单背景 #1A1A1A（深色），统计卡片橙色渐变背景

---

## 隐私保护

GitHub token 等敏感信息存储在 `.claude/settings.local.json`（已 gitignore）。
详见 `.claude/PRIVACY.md`。

---

## 会话复盘

完整的方法论总结见 `.claude/SESSION_REPLAY.md`