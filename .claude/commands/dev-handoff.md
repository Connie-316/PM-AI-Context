# 研发交接 Skill（dev-handoff）

## 使用场景

当用户说"输出研发文档"、"帮我写接口需求"、"技术方案"、"开发需要什么"时调用。
PRD完成后、开发前，执行此Skill输出研发可读的文档。

---

## 核心原则

```
1. 研发交接文档是PRD的"技术翻译版"
2. 不需要写代码，只需要把业务逻辑转成研发能理解的格式
3. 字段说明要完整（类型/长度/是否必填/默认值）
4. 接口设计要明确（请求/响应/错误码）
5. 边界条件和异常要单独说明
```

---

## 执行步骤

### Step 1：读取 PRD 文件

```
确认要输出研发文档的 PRD 是哪个
读取 PRD 内容
提取：数据结构、跳转逻辑、时间规则、验收标准
```

### Step 2：生成接口文档

```markdown
# [功能名] 接口设计文档

## 一、接口总览

| 接口名称 | 请求方式 | 路径 | 说明 |
|---------|---------|------|------|
| 获取弹窗配置 | GET | /api/popup/get | 获取当前有效弹窗 |
| 关闭弹窗 | POST | /api/popup/close | 记录用户关闭行为 |

## 二、接口详情

### 2.1 获取弹窗配置

**请求**
```
GET /api/popup/get?terminal_type=1
```

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| terminal_type | int | 是 | 1=PC端 2=小程序端 |

**响应**
```json
{
  "code": 0,
  "message": "success",
  "data": {
    "id": 1,
    "name": "618大促",
    "display_mode": 2,
    "activity_start_time": "2026-06-01 00:00:00",
    "activity_end_time": "2026-06-30 23:59:59",
    "image_list": [
      {
        "image_url": "https://xxx.com/banner1.jpg",
        "image_start_time": "2026-06-01 00:00:00",
        "image_end_time": "2026-06-10 23:59:59",
        "jump_type": "goods_detail",
        "jump_params": "{\"goods_id\": 1001}"
      }
    ],
    "allow_close": 1,
    "close_expire_days": 7
  }
}
```

**错误码**
| code | 说明 |
|------|------|
| 0 | 成功 |
| 1001 | 无有效弹窗（返回null data） |
| 1002 | 参数错误 |

### 2.2 关闭弹窗

**请求**
```
POST /api/popup/close
Content-Type: application/json

{
  "popup_id": 1,
  "terminal_type": 1
}
```

**响应**
```json
{
  "code": 0,
  "message": "success"
}
```

## 三、数据结构

### 3.1 弹窗配置表（popup_config）

| 字段 | 类型 | 长度 | 必填 | 说明 |
|------|------|------|------|------|
| id | bigint | | 是 | 主键 |
| name | varchar | 100 | 是 | 弹窗名称 |
| terminal_type | tinyint | | 是 | 1=PC端 2=小程序端 |
| display_mode | tinyint | | 是 | 1=单图 2=轮播 |
| activity_start_time | datetime | | 是 | 活动开始时间 |
| activity_end_time | datetime | | 是 | 活动结束时间 |
| image_url | varchar | 500 | 否 | 单图模式图片 |
| jump_type | varchar | 50 | 否 | 跳转类型 |
| jump_params | varchar | 500 | 否 | 跳转参数JSON |
| allow_close | tinyint | | 是 | 0=不可关闭 1=可关闭 |
| close_expire_days | int | | 是 | 默认7 |
| status | tinyint | | 是 | 0=禁用 1=启用 |
| create_time | datetime | | 是 | 创建时间 |
| update_time | datetime | | 是 | 更新时间 |

### 3.2 轮播图片（popup_carousel_image）

| 字段 | 类型 | 说明 |
|------|------|------|
| image_url | varchar | 图片OSS地址 |
| image_start_time | datetime | 图片展示开始时间 |
| image_end_time | datetime | 图片展示结束时间 |
| jump_type | varchar | 跳转类型 |
| jump_params | varchar | 跳转参数JSON |

## 四、业务规则

### 4.1 时间规则

- 图片展示时间必须落在活动整体时间内
- 当前时间不在图片时间窗口内 → 该图片不展示
- 全部图片都不在时间窗口内 → 不展示弹窗

### 4.2 关闭记录

- 用户点击关闭 → 写入本地（popup_id + 时间戳）
- N天内再访问 → 不展示该弹窗
- 关闭记录按端独立（PC和小程序分开）

## 五、异常场景

| 场景 | 处理方式 |
|------|---------|
| 图片加载失败 | 跳过该张，轮播继续；全部失败则不展示 |
| 跳转目标已删除 | 点击无反应，不报错 |
| 重复点击关闭 | 只执行一次，不重复写记录 |

## 六、验收要点

- [ ] 接口返回时间 < 100ms
- [ ] 无有效弹窗时 code=1001，data=null
- [ ] 关闭记录写入本地，非后端存储
- [ ] 图片时间超出活动整体时间时，前端过滤
```

### Step 3：输出研发需求确认单

```markdown
# 研发需求确认单

## 功能：[功能名称]
## PRD版本：[版本号]
## 研发负责人：[待定]
## 预计排期：[X] 天

### 我确认理解以下内容：

1. **核心流程**： [描述]
2. **接口清单**： [X] 个接口
3. **数据结构**： [X] 张表
4. **特殊规则**：
   - [规则1]
   - [规则2]
5. **异常处理**：[描述]
6. **验收标准**：已确认

### 如有疑问请在开发前联系我

研发签字：__________ 日期：__________
PM签字：__________ 日期：__________
```

---

## 输出格式

```
1. 接口设计文档（.md）
2. 研发需求确认单（.md）
3. 如需要可导出为 PDF 发送给研发
```

---

## 与其他 Skill 的配合

```
prd-write 写完 PRD
    ↓
dev-handoff 输出研发文档
    ↓
研发确认签字
    ↓
进入开发阶段
    ↓
测试阶段 → PM 验收业务逻辑
```