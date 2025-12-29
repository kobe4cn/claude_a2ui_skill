# A2UI v0.8 JSON Schema 位置与用途

## 推荐使用的 schema
- 渲染器内置（严格且 LLM 友好）：
  - `renderers/lit/src/0.8/schemas/server_to_client_with_standard_catalog.json`

## 规范目录
- 核心消息 schema：`specification/0.8/json/server_to_client.json`
- 标准 Catalog 定义：`specification/0.8/json/standard_catalog_definition.json`
- 合并后的标准 schema：`specification/0.8/json/server_to_client_with_standard_catalog.json`
- 客户端事件 schema：`specification/0.8/json/client_to_server.json`

## 常见校验要点
- 每条消息只能有一个顶级键。
- surfaceUpdate.components 中 component 只有一个组件类型。
- dataModelUpdate.contents 符合 ValueMap（valueString/valueNumber/valueBoolean/valueMap）。
