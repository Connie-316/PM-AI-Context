# 隐私信息存储说明

GitHub 相关的敏感信息存储在 `settings.local.json` 中。

## 文件位置

`PM-AI-Context/.claude/settings.local.json`

## 内容格式

```json
{
  "github": {
    "owner": "你的GitHub用户名",
    "repo": "PM-AI-Context",
    "token": "ghp_xxxxxxxxxxxxxxxxxxxx"
  }
}
```

## 安全说明

- `settings.local.json` 已在 `.gitignore` 中，不会被推送到 GitHub
- 不在任何 Skill 文件或 CLAUDE.md 中存储 token
- 不在命令行输出中显示 token
- 不在 commit 信息中包含任何敏感信息

## 首次配置

如未配置 token，git-push Skill 会自动提示你配置。

生成 token 方法：
1. 打开 https://github.com/settings/tokens
2. 点击 "Generate new token (classic)"
3. 勾选 `repo` 权限
4. 复制 token 并告诉我

我帮你写入 `settings.local.json`。