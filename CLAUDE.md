# [数智聚模-启泰物料集采商城] - 产品知识库

## 目录结构

| 目录 | 定位 |
|------|------|
| context/ | 产品知识库（已上线功能、架构、团队） |
| workspace/ | 工作区（PRD、需求、讨论） |
| drafts/ | 草稿区（临时想法、方案探索） |
| .claude/commands/ | Skills（AI 标准作业程序） |

## Skill 优先规则

收到任务后，先扫描 .claude/commands/ 是否有对应 Skill。
有则必须调用该 Skill，不直接回答。

---

## Skill 索引

### PRD 与需求分析

| Skill | 触发词 | 使用场景 |
|-------|--------|---------|
| `prd-write.md` | "快速PRD"、"帮我写个PRD" | 单个功能直接写，快速输出 |
| `full-prd.md` | "完整PRD"、"正式PRD" | 必须先完成需求分析，再写完整 PRD |
| `requirements-analysis.md` | "需求分析"、"分析需求" | PRD 撰写前的需求调研与确认 |
| `doc-review.md` | "检查文档"、"审阅PRD"、"去掉冗余"、"修正错误" | 文档修改前审查，自动触发 |
| `doc-archive.md` | "归档"、"上线了" | 功能上线后归档到 context |
| `doc-version.md` | "查版本"、"看历史"、"回退" | 文档版本管理，每次修改自动记录 |

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

---

## 核心路由

- 问"现在产品是什么样的" → 读 context/
- 问"最近在做什么" → 读 workspace/
- 记录临时想法 → 放 drafts/
- 问 UI 规范 → 按端加载对应 skill
- 文档修改后 → 自动调用 doc-review + doc-version
- 功能上线后 → 自动提醒归档（doc-archive）
- 文档确认后 → 自动推送 GitHub（git-push，无需用户说）

---

## 颜色主题速查

| 端 | 主题色 | 辅助色 |
|----|--------|--------|
| 小程序端 | #3370FF 蓝 | 价格 #F5222C / 促销 #FF6B35 |
| 门户商城端 | #1664FF 蓝 | 金刚区橙 #FF7700 |
| 商家端 | #1664FF 蓝 | 统计卡橙 #FF7700 |
| 供应商端 | #1664FF 蓝 | 统计卡橙 #FF7700 |
| 平台端 | #1664FF 蓝 | 统计卡橙 #FF7700 |

**PC 后台通用规范：** 顶部导航/侧边菜单背景 #1A1A1A（深色），统计卡片橙色渐变背景

---

## 完整工作流

```
用户提出需求
    ↓
requirements-analysis（复杂需求先分析）
    ↓
prd-write / full-prd（写 PRD）
    ↓
doc-version（自动保存当前版本到 history/）
    ↓
doc-review（自动审查：对比 + 补充思考 + 全面建议）
    ↓
用户确认修改内容
    ↓
doc-archive（如功能已上线 → 归档到 context）
    ↓
git-push（自动推送 GitHub，无需用户说）
```

---

## 隐私保护

GitHub token 等敏感信息存储在 `.claude/settings.local.json`（已 gitignore）。
详见 `.claude/PRIVACY.md`。

---

## 会话复盘

完整的方法论总结见 `.claude/SESSION_REPLAY.md`