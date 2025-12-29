# A2UI v0.8 Skill 使用方法

本文件提供 a2ui-v0-8 的端到端使用模板，包括：
- 客户端能力声明与扩展激活
- 文本请求生成 UI
- userAction 回传
- 服务端返回 UI 更新

## 0) 基本约定
- A2A 扩展 URI：`https://a2ui.org/a2a-extension/a2ui/v0.8`
- A2UI DataPart mimeType：`application/json+a2ui`
- 标准 Catalog：`https://github.com/google/A2UI/blob/main/specification/0.8/json/standard_catalog_definition.json`

## 1) 客户端 -> 服务端（文本请求，触发 UI 生成）

### HTTP 头（示意）
```
X-A2A-Extensions: https://a2ui.org/a2a-extension/a2ui/v0.8
```

### A2A 请求体（模板）
```json
{
  "message": {
    "kind": "message",
    "messageId": "<uuid>",
    "role": "user",
    "parts": [
      {
        "kind": "text",
        "text": "请生成一个预约表单，包含姓名/邮箱/时间/人数"
      }
    ]
  },
  "metadata": {
    "a2uiClientCapabilities": {
      "supportedCatalogIds": [
        "https://github.com/google/A2UI/blob/main/specification/0.8/json/standard_catalog_definition.json"
      ]
    }
  }
}
```

## 2) 服务端 -> 客户端（A2UI 消息）

服务端通常以 DataPart 返回 A2UI 消息（也可视为 JSONL 流）。

### A2A DataPart 形式（模板）
```json
{
  "kind": "data",
  "mimeType": "application/json+a2ui",
  "data": { "surfaceUpdate": { "surfaceId": "booking-form", "components": [ /* ... */ ] } }
}
```

### JSONL 视角（模板）
```jsonl
{"surfaceUpdate":{"surfaceId":"booking-form","components":[/* ... */]}}
{"dataModelUpdate":{"surfaceId":"booking-form","path":"/form","contents":[/* ... */]}}
{"beginRendering":{"surfaceId":"booking-form","root":"root"}}
```

## 3) 用户交互 -> userAction 回传

### 客户端解析 action.context（示意）
- literal* 直接取值
- path 需要基于 dataContextPath 解析并从数据模型取值

### A2A userAction 请求体（模板）
```json
{
  "message": {
    "kind": "message",
    "messageId": "<uuid>",
    "role": "user",
    "parts": [
      {
        "kind": "data",
        "mimeType": "application/json+a2ui",
        "data": {
          "userAction": {
            "name": "submit_booking",
            "surfaceId": "booking-form",
            "sourceComponentId": "submit",
            "timestamp": "2025-12-16T19:00:00Z",
            "context": {
              "form": {
                "name": "张三",
                "email": "zhang@example.com",
                "datetime": "2025-12-20T19:00:00Z",
                "guests": 2
              }
            }
          }
        }
      }
    ]
  },
  "metadata": {
    "a2uiClientCapabilities": {
      "supportedCatalogIds": [
        "https://github.com/google/A2UI/blob/main/specification/0.8/json/standard_catalog_definition.json"
      ]
    }
  }
}
```

## 4) 服务端响应（确认/更新 UI）

### JSONL 视角（模板）
```jsonl
{"surfaceUpdate":{"surfaceId":"booking-form","components":[{"id":"root","component":{"Card":{"child":"success"}}},{"id":"success","component":{"Column":{"alignment":"center","children":{"explicitList":["icon","title","desc"]}}}},{"id":"icon","component":{"Icon":{"name":{"literalString":"check_circle"}}}},{"id":"title","component":{"Text":{"usageHint":"h2","text":{"literalString":"提交成功"}}}},{"id":"desc","component":{"Text":{"text":{"literalString":"我们已收到你的预约"}}}}]}}
{"beginRendering":{"surfaceId":"booking-form","root":"root"}}
```

## 5) 常见陷阱
- 每条 A2UI 消息只能包含一个顶级键。
- TextField 字段命名可能是 `type` 或 `textFieldType`，务必与实际 renderer/schema 对齐。
- mimeType 必须与服务端一致（推荐 `application/json+a2ui`）。
