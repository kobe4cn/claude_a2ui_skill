# A2UI v0.8 协议要点（生成侧）

## 消息类型与顺序
- beginRendering：指定 surfaceId 与 root，允许附带 styles。
- surfaceUpdate：定义组件列表（扁平结构）。
- dataModelUpdate：写入数据模型（可带 path）。
- deleteSurface：移除 surface。

每条消息必须只有一个顶级键。

## 组件与树结构
- surfaceUpdate.components 是扁平列表，每个组件：
  - id: string
  - component: { "ComponentType": { ...props } }
- 组件树通过 children/child 引用 id 形成。
- children 可以是：
  - explicitList: ["id1", "id2"]
  - template: { componentId, dataBinding }

## 数据模型与 ValueMap
- dataModelUpdate.contents 是 ValueMap 数组：
  - { key, valueString | valueNumber | valueBoolean | valueMap }
- valueMap 支持嵌套，用于对象结构。
- 可选 path 用于设置基路径。

示例（简化）：
```json
{"dataModelUpdate":{"surfaceId":"main","path":"/reservation","contents":[{"key":"guests","valueNumber":2}]}}
```

## 数据绑定（BoundValue）
- 组件属性通常是 literal* 或 path：
  - literalString / literalNumber / literalBoolean
  - path（可为绝对或相对）
- 相对 path 以 dataContextPath 为基准，"." 表示当前上下文。

## 动态列表模板
- children.template.dataBinding 指向数组或 map。
- 每个条目使用 template.componentId 生成子节点。
- 子节点 dataContextPath 会指向条目路径，便于相对绑定。

## 参考实现位置
- 渲染器类型与数据模型：`renderers/lit/src/0.8/types/types.ts`
- 组件属性与 Action：`renderers/lit/src/0.8/types/components.ts`
- 消息处理与模板展开：`renderers/lit/src/0.8/data/model-processor.ts`
