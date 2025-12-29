# A2UI v0.8 JSONL 模板与典型 UI 示例

说明：以下示例均为“JSONL（每行一条消息）”，可直接用于流式发送。示例使用标准 Catalog 与 v0.8 消息结构。

## 1) 表单（Form）示例
```jsonl
{"surfaceUpdate":{"surfaceId":"booking-form","components":[{"id":"root","component":{"Column":{"children":{"explicitList":["title","name","email","datetime","guests","submit"]}}}},{"id":"title","component":{"Text":{"usageHint":"h1","text":{"literalString":"预约信息"}}}},{"id":"name","component":{"TextField":{"label":{"literalString":"姓名"},"text":{"path":"/form/name"}}}},{"id":"email","component":{"TextField":{"label":{"literalString":"邮箱"},"text":{"path":"/form/email"}}}},{"id":"datetime","component":{"DateTimeInput":{"value":{"path":"/form/datetime"},"enableDate":true,"enableTime":true}}},{"id":"guests","component":{"Slider":{"value":{"path":"/form/guests"},"minValue":1,"maxValue":10}}},{"id":"submit-text","component":{"Text":{"text":{"literalString":"提交"}}}},{"id":"submit","component":{"Button":{"child":"submit-text","action":{"name":"submit_booking","context":[{"key":"form","value":{"path":"/form"}}]}}}}]}}
{"dataModelUpdate":{"surfaceId":"booking-form","path":"/form","contents":[{"key":"name","valueString":""},{"key":"email","valueString":""},{"key":"datetime","valueString":""},{"key":"guests","valueNumber":2}]}}
{"beginRendering":{"surfaceId":"booking-form","root":"root"}}
```

## 2) 列表（List + template）示例
```jsonl
{"surfaceUpdate":{"surfaceId":"product-list","components":[{"id":"root","component":{"Column":{"children":{"explicitList":["title","list"]}}}},{"id":"title","component":{"Text":{"usageHint":"h2","text":{"literalString":"推荐商品"}}}},{"id":"list","component":{"List":{"direction":"vertical","children":{"template":{"componentId":"item-card","dataBinding":"/items"}}}}},{"id":"item-card","component":{"Card":{"child":"item-content"}}},{"id":"item-content","component":{"Row":{"alignment":"center","children":{"explicitList":["item-name","item-price","buy"]}}}},{"id":"item-name","component":{"Text":{"text":{"path":"name"}}}},{"id":"item-price","component":{"Text":{"text":{"path":"price"}}}},{"id":"buy-text","component":{"Text":{"text":{"literalString":"购买"}}}},{"id":"buy","component":{"Button":{"child":"buy-text","action":{"name":"buy_item","context":[{"key":"itemId","value":{"path":"id"}}]}}}}]}}
{"dataModelUpdate":{"surfaceId":"product-list","path":"/","contents":[{"key":"items","valueMap":[{"key":"item1","valueMap":[{"key":"id","valueString":"sku_001"},{"key":"name","valueString":"便携水杯"},{"key":"price","valueString":"¥39"}]},{"key":"item2","valueMap":[{"key":"id","valueString":"sku_002"},{"key":"name","valueString":"旅行背包"},{"key":"price","valueString":"¥299"}]}]}]}}
{"beginRendering":{"surfaceId":"product-list","root":"root"}}
```

## 3) 卡片（Card）详情示例
```jsonl
{"surfaceUpdate":{"surfaceId":"profile-card","components":[{"id":"root","component":{"Card":{"child":"content"}}},{"id":"content","component":{"Column":{"children":{"explicitList":["avatar","name","bio","cta"]}}}},{"id":"avatar","component":{"Image":{"url":{"path":"/profile/avatar"},"usageHint":"avatar","fit":"cover"}}},{"id":"name","component":{"Text":{"usageHint":"h3","text":{"path":"/profile/name"}}}},{"id":"bio","component":{"Text":{"text":{"path":"/profile/bio"}}}},{"id":"cta-text","component":{"Text":{"text":{"literalString":"关注"}}}},{"id":"cta","component":{"Button":{"child":"cta-text","action":{"name":"follow_user","context":[{"key":"userId","value":{"path":"/profile/id"}}]}}}}]}}
{"dataModelUpdate":{"surfaceId":"profile-card","path":"/profile","contents":[{"key":"id","valueString":"user_1001"},{"key":"name","valueString":"张可"},{"key":"bio","valueString":"专注产品与体验"},{"key":"avatar","valueString":"https://example.com/avatar.png"}]}}
{"beginRendering":{"surfaceId":"profile-card","root":"root"}}
```

## 4) Modal 示例
```jsonl
{"surfaceUpdate":{"surfaceId":"confirm-modal","components":[{"id":"root","component":{"Column":{"children":{"explicitList":["open","modal"]}}}},{"id":"open-text","component":{"Text":{"text":{"literalString":"打开确认弹窗"}}}},{"id":"open","component":{"Button":{"child":"open-text","action":{"name":"open_modal"}}}},{"id":"modal","component":{"Modal":{"entryPointChild":"open","contentChild":"modal-content"}}},{"id":"modal-content","component":{"Column":{"alignment":"center","children":{"explicitList":["modal-title","modal-desc","dismiss"]}}}},{"id":"modal-title","component":{"Text":{"usageHint":"h3","text":{"literalString":"确认操作"}}}},{"id":"modal-desc","component":{"Text":{"text":{"literalString":"是否继续执行？"}}}},{"id":"dismiss-text","component":{"Text":{"text":{"literalString":"关闭"}}}},{"id":"dismiss","component":{"Button":{"child":"dismiss-text","action":{"name":"dismiss_modal"}}}}]}}
{"beginRendering":{"surfaceId":"confirm-modal","root":"root"}}
```

## 5) Tabs 示例
```jsonl
{"surfaceUpdate":{"surfaceId":"settings-tabs","components":[{"id":"root","component":{"Column":{"children":{"explicitList":["title","tabs"]}}}},{"id":"title","component":{"Text":{"usageHint":"h2","text":{"literalString":"设置"}}}},{"id":"tab-general","component":{"Column":{"children":{"explicitList":["general-title","general-desc"]}}}},{"id":"general-title","component":{"Text":{"usageHint":"h4","text":{"literalString":"通用设置"}}}},{"id":"general-desc","component":{"Text":{"text":{"literalString":"账号与通知设置"}}}},{"id":"tab-security","component":{"Column":{"children":{"explicitList":["security-title","security-desc"]}}}},{"id":"security-title","component":{"Text":{"usageHint":"h4","text":{"literalString":"安全设置"}}}},{"id":"security-desc","component":{"Text":{"text":{"literalString":"登录与隐私设置"}}}},{"id":"tabs","component":{"Tabs":{"tabItems":[{"title":{"literalString":"通用"},"child":"tab-general"},{"title":{"literalString":"安全"},"child":"tab-security"}]}}}]}}
{"beginRendering":{"surfaceId":"settings-tabs","root":"root"}}
```

## 6) MultipleChoice + CheckBox 示例
```jsonl
{"surfaceUpdate":{"surfaceId":"preferences","components":[{"id":"root","component":{"Column":{"children":{"explicitList":["title","topics","marketing","save"]}}}},{"id":"title","component":{"Text":{"usageHint":"h3","text":{"literalString":"偏好设置"}}}},{"id":"topics","component":{"MultipleChoice":{"selections":{"path":"/prefs/topics"},"options":[{"label":{"literalString":"产品更新"},"value":"product"},{"label":{"literalString":"行业动态"},"value":"industry"},{"label":{"literalString":"活动通知"},"value":"events"}],"maxAllowedSelections":2}}},{"id":"marketing","component":{"CheckBox":{"label":{"literalString":"允许营销邮件"},"value":{"path":"/prefs/marketing"}}}},{"id":"save-text","component":{"Text":{"text":{"literalString":"保存设置"}}}},{"id":"save","component":{"Button":{"child":"save-text","action":{"name":"save_prefs","context":[{"key":"prefs","value":{"path":"/prefs"}}]}}}}]}}
{"dataModelUpdate":{"surfaceId":"preferences","path":"/prefs","contents":[{"key":"topics","valueString":"[]"},{"key":"marketing","valueBoolean":false}]}}
{"beginRendering":{"surfaceId":"preferences","root":"root"}}
```

## 7) 二步确认流程（请求 -> 成功）示例
**Step A: 请求确认 UI**
```jsonl
{"surfaceUpdate":{"surfaceId":"checkout","components":[{"id":"root","component":{"Column":{"children":{"explicitList":["title","summary","confirm"]}}}},{"id":"title","component":{"Text":{"usageHint":"h2","text":{"literalString":"确认支付"}}}},{"id":"summary","component":{"Card":{"child":"summary-content"}}},{"id":"summary-content","component":{"Column":{"children":{"explicitList":["item","total"]}}}},{"id":"item","component":{"Text":{"text":{"path":"/order/item"}}}},{"id":"total","component":{"Text":{"usageHint":"h4","text":{"path":"/order/total"}}}},{"id":"confirm-text","component":{"Text":{"text":{"literalString":"确认并支付"}}}},{"id":"confirm","component":{"Button":{"child":"confirm-text","action":{"name":"confirm_payment","context":[{"key":"order","value":{"path":"/order"}}]}}}}]}}
{"dataModelUpdate":{"surfaceId":"checkout","path":"/order","contents":[{"key":"item","valueString":"会议室预订（2小时）"},{"key":"total","valueString":"¥300"}]}}
{"beginRendering":{"surfaceId":"checkout","root":"root"}}
```
**Step B: 成功 UI（服务端收到 userAction 后返回）**
```jsonl
{"surfaceUpdate":{"surfaceId":"checkout","components":[{"id":"root","component":{"Card":{"child":"success"}}},{"id":"success","component":{"Column":{"alignment":"center","children":{"explicitList":["icon","title","desc"]}}}},{"id":"icon","component":{"Icon":{"name":{"literalString":"check_circle"}}}},{"id":"title","component":{"Text":{"usageHint":"h2","text":{"literalString":"支付成功"}}}},{"id":"desc","component":{"Text":{"text":{"literalString":"订单已确认，请查收邮件"}}}}]}}
{"beginRendering":{"surfaceId":"checkout","root":"root"}}
```

使用建议：
- 表单类 UI：为 submit 按钮配置 action.context，回传整个表单路径。
- 列表类 UI：优先使用 template + dataBinding，数据用 valueMap（Map）或 JSON 字符串数组。
- Modal：entryPointChild 负责打开，contentChild 是弹窗内容组件。
