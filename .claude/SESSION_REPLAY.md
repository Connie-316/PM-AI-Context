# 本次会话复盘：AI 工作流方法论总结

> 基于今天与你的完整工作会话生成，记录我们做了什么、为什么做、以及可以复用的工作模式。

---

## 一、我们今天做了什么

### 1.1 项目结构搭建（从零）

我们搭建了一个完整的 PM AI 工作台：

```
PM-AI-Context/
├── CLAUDE.md                    # 总索引（AI 的地图）
├── context/                     # 产品知识库
│   ├── 01_产品架构/
│   │   ├── 产品简介.md           # 产品定位、用户、端说明
│   │   ├── 术语表.md             # 业务术语（含账期/供应链金融等）
│   │   └── CLAUDE.md
│   ├── 02_功能模块/
│   │   ├── CLAUDE.md
│   │   ├── 已上线功能列表.md
│   │   └── history/
│   └── 03_技术决策/
│       └── ADR-001_弹窗优先级规则.md  # 重要业务决策记录
├── workspace/
│   └── prd/
│       ├── CLAUDE.md
│       ├── history/
│       ├── 首页营销弹窗配置_20260521.md  # 第一个 PRD
│       └── _PRD状态追踪.md
├── drafts/
│   └── IDEA_想法记录模板.md      # 灵感记录模板
├── templates/                   # 文档模板库
│   ├── PRD_标准模板.md
│   ├── 需求分析模板.md
│   ├── 会议纪要模板.md
│   └── 上线检查清单.md
└── .claude/
    ├── settings.local.json      # GitHub token（私密，gitignore）
    ├── PRIVACY.md               # 隐私保护说明
    ├── SESSION_REPLAY.md        # 本文件
    └── commands/                # Skills（13个）
        ├── requirements-analysis.md  # 需求分析
        ├── full-prd.md         # 完整 PRD（需先分析）
        ├── prd-write.md        # 快速 PRD（直接写）
        ├── doc-review.md       # 文档审查
        ├── doc-archive.md      # 文档归档
        ├── doc-version.md      # 版本管理
        ├── git-push.md         # GitHub 推送
        ├── ui-spec-miniprogram.md   # 小程序端 UI
        ├── ui-spec-portal.md        # 门户商城端 UI
        ├── ui-spec-merchant.md      # 商家端 UI
        ├── ui-spec-supplier.md      # 供应商端 UI
        ├── ui-spec-platform.md       # 平台端 UI
        └── ui-demo-preview.html      # 可视化 Demo
```

### 1.2 需求文档实战

用 prd-write Skill 写了"首页营销弹窗配置"PRD，涵盖：
- 单图/轮播两种模式
- PC端和小程序端不同尺寸规范
- 活动整体时间和图片独立时间两层时间逻辑
- 手动关闭 + 7天不展示逻辑
- 完整的验收标准

### 1.3 GitHub 已推送

所有文件已推送到 https://github.com/Connie-316/PM-AI-Context
Token 存在 `settings.local.json`（gitignore，不上传）

---

## 二、核心方法论：Context 工程

### 2.1 为什么 Context 决定了 AI 输出质量

我们做了一个对比实验：

```
❌ 低质量输入：帮我写个 PRD
✅ 中质量输入：描述背景 + 让 AI 理解你要做什么
✅ 高质量输入：完整的 Context（背景/架构/约束/竞品/目标用户）
```

**结论："输入决定输出"。模型越好，输入的质量差异越大。**

### 2.2 三个关键公式

```
Agent = Skill × Context × CLAUDE.md
文档价值 = Context 积累 × 时间复利
AI 输出质量 = 你给它的 Context 厚度
```

### 2.3 Context 的分类

| 类型 | 存放位置 | 更新频率 | AI 用途 |
|------|---------|---------|---------|
| 产品知识（已确定事实） | context/ | 上线后更新 | 回答"现在是什么样" |
| 工作进展（规划中） | workspace/ | 持续更新 | 回答"最近在做什么" |
| 临时想法 | drafts/ | 随时新建 | 记录灵感，不让 AI 知道 |
| 标准操作程序 | .claude/commands/ | 稳定不变 | 告诉 AI 怎么做 |
| 模板文件 | templates/ | 稳定不变 | 直接复用，减少重复劳动 |

---

## 三、Skill 设计方法论

### 3.1 Skill 是什么

Skill = 写好一次、反复调用的 SOP。

触发方式：自然语言触发（不说斜杠命令）。

### 3.2 Skill 结构范式

每个 Skill 文件包含：

```markdown
# Skill 名称

## 使用场景
什么时候用这个 Skill

## 前置条件（如有）
需要什么输入才能工作

## 执行步骤
步骤1：做什么
步骤2：做什么
步骤3：做什么

## 输出格式
产出的文档格式

## 核心规则
几条最重要的约束

## 禁止操作
什么情况不能用/不能做
```

### 3.3 你的 Skill 体系设计

```
PRD 类 Skill（3个）：
├── requirements-analysis  → 分析需求（前置）
├── full-prd             → 完整 PRD（接分析）
└── prd-write            → 快速 PRD（直接写）

文档类 Skill（3个）：
├── doc-review            → 文档审查（每次修改自动触发）
├── doc-version           → 版本管理（保存历史）
└── doc-archive           → 归档（上线后移到 context）

UI 规范 Skill（5个，按端分）：
├── ui-spec-miniprogram   → 小程序端（#3370FF）
├── ui-spec-portal        → 门户商城端（#1664FF）
├── ui-spec-merchant      → 商家端（#1664FF）
├── ui-spec-supplier      → 供应商端（#1664FF）
└── ui-spec-platform      → 平台端（#1664FF）

工具类 Skill（2个）：
├── git-push              → GitHub 推送
└── ui-demo-preview       → UI 规范可视化预览
```

---

## 四、文档修改的标准工作流

### 4.1 修改前思考（每次文档修改必问）

```
1. 这个文档是给谁看的？（研发/领导/评审/自己）
2. 他看完需要知道什么？（目标/做什么/怎么做）
3. 现有内容有没有缺失？（背景/规则/异常/验收）
4. 有没有冗余重复？（同一句话说了两遍）
5. 格式是否统一？（表格/列表/标题层级）
6. 和相关文档是否一致？（术语/字段/状态）
```

### 4.2 修改后必做

```
1. doc-version 保存当前版本到 history/（自动）
2. doc-review 审查（自动检查 6 个维度）
3. 确认无问题后更新原文件
4. git-push 推送到 GitHub（自动）
```

### 4.3 文档命名规范

```
PRD 文件：workspace/prd/[功能名称]_[日期].md
需求分析：workspace/prd/需求分析/[功能名称]_[日期].md
归档后：  context/02_功能模块/[功能名称].md
版本历史：workspace/prd/history/[功能名称]_[日期]_v1.md
```

---

## 五、PRD 写作的标准思考路径

写每个 PRD 时，思考以下 8 个问题：

```
1. 这个需求解决什么问题？（背景）
2. 做完之后业务会有什么不同？（目标）
3. 谁会用这个功能？（用户角色）
4. 用户用这个功能的典型路径是什么？（核心流程）
5. 有哪些配置项，每项的值域是什么？（功能需求）
6. 边界条件是什么？异常情况怎么处理？（异常情况）
7. 怎么验证做对了？（验收标准）
8. 这个功能依赖哪些模块？（上下游耦合）
```

---

## 六、UI 规范的标准思考路径

分析任何 UI 截图时，按以下维度提取：

```
1. 颜色体系
   - 主色（按钮/链接/选中态）
   - 功能色（成功/警告/错误/待处理各有颜色）
   - 中性色（标题/正文/辅助/分割线/背景）

2. 布局结构
   - 整体是左右分栏还是上下？
   - 各区域尺寸/比例
   - 间距规范（卡片间距/内边距）

3. 组件样式
   - 按钮（圆角/高度/背景/文字）
   - 输入框（高度/圆角/聚焦态）
   - 卡片（圆角/阴影/内边距）
   - 表格（行高/表头样式/边框）

4. 字体规范
   - 各级别字号
   - 字重（标题600/正文400）
   - 色值（标题#333/正文#595/辅助#8C8C8C）

5. 状态规范
   - 状态标签颜色系统
   - 选中/未选中/hover 态的颜色差异
```

---

## 七、GitHub 推送

已完成推送：
- 所有文件推送到 https://github.com/Connie-316/PM-AI-Context
- GitHub token 存在 `.claude/settings.local.json`（已 gitignore）
- 推送后 git-push 自动执行，无需用户说

---

## 八、下一步你可以做什么

1. **补充 context** — 把更多产品背景写进 context/
2. **补充竞品分析** — 分析嘉立创、怡合达、云汉芯城等竞争对手
3. **把 PRD 归档** — 首页弹窗上线后，搬到 context/02_功能模块/
4. **补充门户端 UI 规范** — 从 MasterGo 导出截图补充 portal 规范
5. **开始用** — 遇到新需求时，用 `prd-write` 快速写 PRD
6. **把同事拉进来** — 共享同一个 Context 仓库，大家的 AI 都能对齐