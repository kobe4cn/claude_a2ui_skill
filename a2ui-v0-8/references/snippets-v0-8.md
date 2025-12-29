# A2UI v0.8 可复用片段库

使用方式：
- 建议为所有 id 增加前缀（如 `hdr-`, `cta-`, `card-`），避免与其他组件冲突。
- 片段只提供组件定义，需按实际 surfaceId 与 dataModelUpdate 补齐数据。

## 1) 标题区（Header）
```json
[
  {"id":"hdr-title","component":{"Text":{"usageHint":"h1","text":{"path":"/header/title"}}}},
  {"id":"hdr-sub","component":{"Text":{"text":{"path":"/header/subtitle"}}}},
  {"id":"hdr-wrap","component":{"Column":{"children":{"explicitList":["hdr-title","hdr-sub"]}}}}
]
```

## 2) 主 CTA 行（CTA Row）
```json
[
  {"id":"cta-primary-text","component":{"Text":{"text":{"literalString":"立即开始"}}}},
  {"id":"cta-primary","component":{"Button":{"child":"cta-primary-text","action":{"name":"primary_action"}}}},
  {"id":"cta-secondary-text","component":{"Text":{"text":{"literalString":"了解更多"}}}},
  {"id":"cta-secondary","component":{"Button":{"child":"cta-secondary-text","action":{"name":"secondary_action"}}}},
  {"id":"cta-row","component":{"Row":{"distribution":"center","alignment":"center","children":{"explicitList":["cta-primary","cta-secondary"]}}}}
]
```

## 3) 结果卡片（Result Card）
```json
[
  {"id":"card-image","component":{"Image":{"url":{"path":"imageUrl"},"fit":"cover","usageHint":"smallFeature"}}},
  {"id":"card-title","component":{"Text":{"usageHint":"h3","text":{"path":"title"}}}},
  {"id":"card-desc","component":{"Text":{"text":{"path":"desc"}}}},
  {"id":"card-cta-text","component":{"Text":{"text":{"literalString":"查看"}}}},
  {"id":"card-cta","component":{"Button":{"child":"card-cta-text","action":{"name":"view_detail","context":[{"key":"id","value":{"path":"id"}}]}}}},
  {"id":"card-body","component":{"Column":{"children":{"explicitList":["card-title","card-desc","card-cta"]}}}},
  {"id":"card-row","component":{"Row":{"alignment":"center","children":{"explicitList":["card-image","card-body"]}}}},
  {"id":"card","component":{"Card":{"child":"card-row"}}}
]
```

## 4) 空状态（Empty State）
```json
[
  {"id":"empty-icon","component":{"Icon":{"name":{"literalString":"inbox"}}}},
  {"id":"empty-title","component":{"Text":{"usageHint":"h3","text":{"literalString":"暂无结果"}}}},
  {"id":"empty-desc","component":{"Text":{"text":{"literalString":"尝试调整筛选条件"}}}},
  {"id":"empty-wrap","component":{"Column":{"alignment":"center","children":{"explicitList":["empty-icon","empty-title","empty-desc"]}}}}
]
```

## 5) Modal 内容区（Content Only）
```json
[
  {"id":"modal-title","component":{"Text":{"usageHint":"h3","text":{"literalString":"操作提示"}}}},
  {"id":"modal-desc","component":{"Text":{"text":{"literalString":"该操作不可撤销"}}}},
  {"id":"modal-ok-text","component":{"Text":{"text":{"literalString":"确认"}}}},
  {"id":"modal-ok","component":{"Button":{"child":"modal-ok-text","action":{"name":"confirm"}}}},
  {"id":"modal-cancel-text","component":{"Text":{"text":{"literalString":"取消"}}}},
  {"id":"modal-cancel","component":{"Button":{"child":"modal-cancel-text","action":{"name":"cancel"}}}},
  {"id":"modal-actions","component":{"Row":{"distribution":"end","children":{"explicitList":["modal-cancel","modal-ok"]}}}},
  {"id":"modal-content","component":{"Column":{"children":{"explicitList":["modal-title","modal-desc","modal-actions"]}}}}
]
```

## 6) 列表模板（配合 List.template）
```json
[
  {"id":"list-item-title","component":{"Text":{"text":{"path":"title"}}}},
  {"id":"list-item-sub","component":{"Text":{"text":{"path":"subtitle"}}}},
  {"id":"list-item","component":{"Column":{"children":{"explicitList":["list-item-title","list-item-sub"]}}}}
]
```

提示：用于 template.componentId 时，list-item 及其子组件 id 会自动带后缀，避免冲突。
