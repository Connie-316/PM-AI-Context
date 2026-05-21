# GitHub 推送 Skill（git-push）

## 使用场景
当用户说"推送"、"提交"、"推送到GitHub"、"推上去"时调用。

**隐私信息存储在 `.claude/settings.local.json`（gitignored，不会上传）：**
```json
{
  "github": {
    "owner": "你的GitHub用户名",
    "repo": "PM-AI-Context",
    "token": "ghp_xxxxxxxxxxxxxxxxxxxx"
  }
}
```

> 首次使用需要配置 token。可在 https://github.com/settings/tokens 生成，勾选 `repo` 权限。

---

## 执行步骤

### 首次配置（如未配置）

1. 询问用户 GitHub 用户名、仓库名、token
2. 将信息存入 `.claude/settings.local.json`
3. 生成仓库地址：`https://github.com/{owner}/{repo}.git`

### 推送流程

```
Step 1: 读取 settings.local.json 获取 GitHub 配置
    ↓
Step 2: git add . （不强制全部，可指定文件）
    ↓
Step 3: 自动生成 commit 信息
    ↓
Step 4: git remote 获取仓库地址
    ↓
Step 5: 如无 remote → 提示用户先在 GitHub 创建仓库
    ↓
Step 6: git push 推送到 GitHub
    ↓
Step 7: 返回推送结果（成功/失败/冲突）
```

### 推送模式

| 模式 | 触发词 | 说明 |
|------|--------|------|
| **增量推送** | "推送"（默认） | 只推送有变动的文件，不碰其他文件 |
| **全量推送** | "强制推送" | git add -A，覆盖式推送 |
| **指定推送** | "只推送这个文件" | 追加文件路径，只推指定的 |

### 增量推送规则

```
✅ 推送：修改过的文件、新增的文件
✅ 更新：已在 Git 跟踪但本地有变动的文件
❌ 不动：已在 GitHub 上存在的其他文件（不覆盖、不删除）
❌ 不动：.DS_Store、node_modules 等忽略文件
```

### 自动 commit 信息格式

```
docs: 更新 ui-spec-merchant.md（主色统一为 #1664FF）
      - 商家端 UI 规范补充完整
      - 统计卡片样式更新
      - 布局结构图补充
```

---

## GitHub 仓库操作规则（重要）

### 绝对禁止操作

❌ 不删除 GitHub 上已存在的任何文件
❌ 不修改 GitHub 上已存在的其他文件（只更新我方修改过的文件）
❌ 不执行 force push
❌ 不执行 git push --force
❌ 不操作 pm_agent 仓库（只操作 PM-AI-Context）

### 安全操作范围

```
✅ 新增文件 → 推送到 GitHub
✅ 修改文件 → 推送到 GitHub（只更新修改的部分）
✅ 删除文件 → 仅当文件在本地也被删除时才删除远程（慎重）
```

### 冲突处理

```
推送时如果遇到冲突：
1. 显示冲突文件列表
2. 询问用户选择：
   - "保留远程" → 不推送冲突文件
   - "保留本地" → 覆盖远程版本（需用户明确确认）
   - "手动处理" → 退出，让用户手动解决
```

---

## 自动推送触发

### 触发条件

以下情况**自动触发推送**，不需要用户说：
1. 用户说"写完了 PRD" 或 "帮我写个 PRD" 并确认内容后
2. 用户说"更新了 UI 规范" 并确认后
3. 用户说"归档" 并完成归档后
4. 用户说"推送"（手动触发）

### 不自动推送的情况

- 草稿阶段（drafts/ 里的内容不自动推）
- 未经用户确认的修改
- 仅查询类的操作（读文档、看内容）

---

## 输出格式

```markdown
## GitHub 推送结果

**仓库**：`https://github.com/{owner}/{repo}.git`
**分支**：`main`
**推送时间**：[时间]

### 本次推送文件

| 文件 | 操作 |
|------|------|
| .claude/commands/ui-spec-merchant.md | 更新 |
| workspace/prd/首页营销弹窗配置_20260521.md | 新增 |

### Commit 信息

```
docs: 更新商家端 UI 规范

- 主色统一为 #1664FF
- 补充商家端统计卡片样式
- 补充布局结构图
```

### 状态

✅ 推送成功
🌐 https://github.com/{owner}/{repo}/tree/main

---

**注意**：推送后 GitHub 上原有的其他文件不会被修改或删除。
```

---

## 隐私保护

- GitHub token 存储在 `.claude/settings.local.json`（已 gitignore）
- 不在 CLAUDE.md 或任何 Skill 文件中存储 token
- 不在命令行输出中显示 token
- commit 信息不包含任何敏感信息

---

## 与其他 Skill 的配合

```
prd-write 完成 PRD
    ↓
doc-review 审查
    ↓
用户确认内容
    ↓
如需归档 → doc-archive
    ↓
git-push 自动推送（无需用户说）
```

---

## 故障处理

| 问题 | 处理方式 |
|------|---------|
| 未配置 token | 提示用户配置，停止推送 |
| 仓库不存在 | 提示用户在 GitHub 先创建仓库 |
| 无 remote | 显示命令让用户添加 remote |
| 推送失败 | 显示错误原因，重新尝试或提示手动处理 |