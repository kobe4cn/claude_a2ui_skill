# A2UI v0.8 客户端事件（userAction）

## userAction 结构
```json
{
  "userAction": {
    "name": "confirm",
    "surfaceId": "booking",
    "sourceComponentId": "submit-btn",
    "timestamp": "2025-12-16T19:00:00Z",
    "context": {
      "details": {
        "datetime": "2025-12-16T19:00:00Z",
        "guests": 3
      }
    }
  }
}
```

字段说明：
- name：来自组件 action.name
- surfaceId：事件所在 surface
- sourceComponentId：触发组件 id
- timestamp：ISO 8601
- context：从 action.context 解析出的键值对象

## action.context 解析步骤（客户端）
1. 遍历 action.context 数组（每项包含 key + value）。
2. 若 value 是 literalString/literalNumber/literalBoolean，直接赋值。
3. 若 value 是 path：
   - 以 dataContextPath 解析相对路径
   - 从数据模型取值并写入 context

参考实现：`samples/client/lit/shell/app.ts` 中的 @a2uiaction 处理逻辑。
