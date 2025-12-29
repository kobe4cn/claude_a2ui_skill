# 端到端事件流程（简化）

1. 客户端收到服务端 JSONL 消息，处理 surfaceUpdate/dataModelUpdate。
2. 收到 beginRendering 后开始渲染。
3. 用户交互触发 action：客户端构建 userAction。
4. 通过 A2A 发送 userAction（DataPart）。
5. 服务端处理后返回新的 A2UI 消息，客户端应用更新。

示例可参考：
- 数据流说明：`docs/concepts/data-flow.md`
- Lit 客户端事件处理：`samples/client/lit/shell/app.ts`
- 后端处理 userAction：`samples/agent/adk/contact_lookup/agent_executor.py`
