# PM-AI-Context 工作台

## 定位

启泰数智聚模物料集采商城的 AI 辅助产品工作空间，用于沉淀和管理产品知识、需求文档、团队决策。

## 目录结构

| 目录 | 定位 | 说明 |
|------|------|------|
| [context/](context/01_产品架构/CLAUDE.md) | 产品知识库（已上线功能、架构、团队） | 上线后的事实沉淀 |
| [workspace/](workspace/CLAUDE.md) | 工作区（PRD、需求、讨论） | 进行中的工作 |
| [drafts/](drafts/CLAUDE.md) | 草稿区（临时想法、方案探索） | 还没形成正式需求 |
| [templates/](templates/CLAUDE.md) | 文档模板库 | PRD、会议纪要、检查清单 |
| [.claude/commands/](.claude/commands/) | Skills（AI 标准作业程序） | 技能触发词 |

## 快速入口

| 文件 | 什么时候看 |
|------|-----------|
| [START_HERE.md](START_HERE.md) | 第一次用 / 忘了怎么用 |
| [SKILL_GUIDE.md](SKILL_GUIDE.md) | 忘记了触发词 / 不知道用哪个 |

## Skills 入口（按使用场景）

| 触发词 | Skill | 使用场景 |
|--------|-------|---------|
| "记录这个"、"保存这个" | [.claude/commands/ingest.md](.claude/commands/ingest.md) | 用户粘贴内容时路由到正确位置 |
| "健康检查"、"诊断" | [.claude/commands/diagnose.md](.claude/commands/diagnose.md) | 知识库健康诊断 |
| "Bootstrap"、"访谈" | [.claude/commands/bootstrap.md](.claude/commands/bootstrap.md) | 系统性提取业务知识 |
| "快速PRD"、"帮我写个PRD" | [.claude/commands/prd-write.md](.claude/commands/prd-write.md) | 单个功能直接写 |
| "完整PRD"、"正式PRD" | [.claude/commands/full-prd.md](.claude/commands/full-prd.md) | 必须先完成需求分析 |
| "输出研发文档"、"写接口需求" | [.claude/commands/dev-handoff.md](.claude/commands/dev-handoff.md) | PRD完成后开发前 |
| "TAPD对齐"、"迭代乱了" | [.claude/commands/tapd-sync.md](.claude/commands/tapd-sync.md) | 同步 TAPD 迭代 |
| "月度规划"、"关键任务规划" | [.claude/commands/monthly-plan.md](.claude/commands/monthly-plan.md) | 每月25号规划 |
| "周复盘"、"本周总结" | [.claude/commands/weekly-review.md](.claude/commands/weekly-review.md) | 每周五复盘 |
| "检查文档"、"审阅PRD" | [.claude/commands/doc-review.md](.claude/commands/doc-review.md) | 文档修改后审查 |
| "查版本"、"看历史" | [.claude/commands/doc-version.md](.claude/commands/doc-version.md) | 版本管理 |
| "归档"、"上线了" | [.claude/commands/doc-archive.md](.claude/commands/doc-archive.md) | 功能上线后归档 |
| "小程序UI"、"商城UI" | [.claude/commands/ui-spec-miniprogram.md](.claude/commands/ui-spec-miniprogram.md) | 小程序端 UI |
| "门户端UI"、"官网UI" | [.claude/commands/ui-spec-portal.md](.claude/commands/ui-spec-portal.md) | 门户商城 PC/H5 端 |
| "商家端UI" | [.claude/commands/ui-spec-merchant.md](.claude/commands/ui-spec-merchant.md) | 商家端后台 |
| "供应商端UI" | [.claude/commands/ui-spec-supplier.md](.claude/commands/ui-spec-supplier.md) | 供应商端后台 |
| "平台端UI"、"运营后台" | [.claude/commands/ui-spec-platform.md](.claude/commands/ui-spec-platform.md) | 平台运营后台 |

## 工作流

```
新需求进入
    ↓
登记到 workspace/需求池管理.md
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
进入开发 → 上线 → doc-archive 归档
```

## 隐私

GitHub token 存储在 `.claude/settings.local.json`（已 gitignore），永远不写入 Skill 文件。