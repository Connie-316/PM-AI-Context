# 供应商端 UI 规范 Skill（ui-spec-supplier）

## 使用场景
当用户提到"供应商端UI"、"供应商后台UI"时调用。

## 规范说明

供应商端与商家端共用同一套主题规范。以下为完整规范内容，引用 ui-spec-merchant.md 的全部定义。

---

## 技术栈

| 技术 | 说明 |
|------|------|
| 框架 | React + Ant Design 5 |
| 构建 | Vite |
| 主题色 | #1664FF（蓝色） |
| 辅助色 | 橙色 #FF6B00（统计卡）、价格红 #F5222D |

---

## 颜色规范（蓝色主题）

```css
/* 主题色 */
--color-primary: #1664FF;
--color-primary-hover: #1458DB;

/* 主按钮 */
.ant-btn-primary {
  background: #1664FF !important;
  border-color: #1664FF !important;
}
.ant-btn-primary:hover {
  background: #1458DB !important;
}

/* 顶部导航 / 侧边菜单背景 */
background: #1A1A1A;

/* 统计卡片背景（橙色） */
.stat-card-orange {
  background: linear-gradient(135deg, #FF7700, #FF6B00);
}

/* 菜单选中态 */
.ant-menu-item-selected {
  border-left: 3px solid #1664FF;
  color: #1664FF !important;
  background: rgba(22,100,255,0.15) !important;
}
```

### 中性色

| 色值 | 用途 |
|------|------|
| #1A1A1A | 顶部导航/侧边菜单背景 |
| #333333 | 标题黑 |
| #595959 | 正文灰 |
| #8C8C8C | 辅助灰 |
| #D9D9D9 | 边框灰 |
| #FAFAFA | 表格表头背景 |
| #F5F5F5 | 页面背景 |
| #FFFFFF | 卡片/表格背景 |

### 功能色

| 色值 | 用途 |
|------|------|
| #F5222D | 错误/价格红 |
| #FAAD14 | 警告/待处理 |
| #52C41A | 成功/已完成 |
| #FF6B00 | 橙色统计卡 |

---

## 布局规范

| 元素 | 规范 |
|------|------|
| 顶部导航 | 高 56px，背景 #1A1A1A，白色文字 |
| 侧边菜单 | 宽 200px，背景 #1A1A1A，白色文字 |
| 侧边菜单选中 | 左侧 3px #1664FF，文字 #1664FF |
| 内容区背景 | #F5F5F5 |
| 表格行高 | 48px |
| 分页 | 固定底部，不随列表滚动 |

---

## 字体规范

| 层级 | 字号 | 字重 |
|------|------|------|
| 顶部导航 | 14px | 500 |
| 侧边菜单一级 | 14px | 500 |
| 侧边菜单二级 | 13px | 400 |
| 页面标题 | 18px | 600 |
| 表格表头 | 13px | 600 |
| 表格内容 | 13px | 400 |
| 正文 | 14px | 400 |
| 辅助文字 | 12px | 400 |

---

## 圆角规范

| 元素 | 圆角 |
|------|------|
| 按钮 | 4px |
| 输入框 | 4px |
| 卡片 | 8px |
| 弹窗 | 8px |

---

## PC 端 Demo 生成

如需生成供应商端 Demo 页面，说"帮我做一个[功能名]页面"，AI 将使用本规范生成蓝色主题的 React + Ant Design 代码。