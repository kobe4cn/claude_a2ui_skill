# A2UI v0.8 标准组件（概览）

组件列表（标准 Catalog）：
AudioPlayer, Button, Card, CheckBox, Column, DateTimeInput, Divider, Icon, Image, List, Modal, MultipleChoice, Row, Slider, Tabs, Text, TextField, Video

关键属性提示（非完整）：
- Text: text, usageHint
- Image: url, fit?, usageHint?
- Icon: name
- Row/Column: children, distribution?, alignment?
- List: children, direction?, alignment?
- Card: child 或 children
- Tabs: tabItems[{title, child}]
- Modal: entryPointChild, contentChild
- Button: child, action
- CheckBox: label, value
- TextField: label, text?, type?/textFieldType?
- DateTimeInput: value, enableDate?, enableTime?
- MultipleChoice: selections, options, maxAllowedSelections?
- Slider: value, minValue?, maxValue?

注意：TextField 字段在不同文件中有 type 与 textFieldType 的差异，使用前对齐实际 renderer/schema。

参考文件：
- 标准 Catalog 定义：`specification/0.8/json/standard_catalog_definition.json`
- Lit 渲染器组件类型：`renderers/lit/src/0.8/types/components.ts`
