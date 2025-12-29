# A2A 扩展与能力协商（A2UI v0.8）

## 扩展 URI
- `https://a2ui.org/a2a-extension/a2ui/v0.8`

## 激活方式
- HTTP/JSON-RPC：请求头 `X-A2A-Extensions` 包含上述 URI
- gRPC：metadata 同名字段

## 客户端能力（a2uiClientCapabilities）
每次 A2A 消息都应带上：
```json
{
  "supportedCatalogIds": [
    "https://github.com/google/A2UI/blob/main/specification/0.8/json/standard_catalog_definition.json"
  ],
  "inlineCatalogs": []
}
```

## DataPart 编码
- mimeType：`application/json+a2ui`
- data：单条 A2UI 消息（userAction 或 server->client 的任一消息）

注意：样例代码可能使用 `application/json+a2aui`，需与服务端保持一致。

参考文件：
- 规范说明：`specification/0.8/docs/a2ui_extension_specification.md`
- 客户端事件 schema：`specification/0.8/json/client_to_server.json`
- 样例客户端：`samples/client/lit/shell/client.ts`
