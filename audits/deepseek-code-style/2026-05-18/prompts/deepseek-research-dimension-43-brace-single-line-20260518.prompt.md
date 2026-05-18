深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. braces for single line control flow code style always use braces if for while
2. curly braces single statement if code review style guide
3. ESLint curly rule multi-line all always code appearance
4. Checkstyle NeedBraces if for while single line control flow
5. K&R Allman brace style same line next line separate formatting dimension
6. single line control flow no braces code style visual indicators
7. whether brace newline style is separate from braces for single-line control flow

我们需要同时探索多个方向, 针对研究中的缺口进行补充搜索。

当上下文未提供必要属性所需的数据信息时：
- 若该信息**无法通过上下文推断或合理派生**，则使用显式标记默认占位填充（templated placeholder, UPPER_CASE）提示用户补充
- 若该信息**可通过上下文中的其他信息推断得出**，则可直接使用推断值
- **禁止**自行生成"看似真实"但实际未提供的具体数据（如虚构的ID、时间戳、用户名等）

附加格式要求:

1. 用摘要或关键词概括那个连续段落的核心内容，并放在问题之前, 总-分的写作方法。
2. 在连续段落的开头或结尾加入信号词, 信号词标记方式与回复格式保持一致, 比如markdown时请使用 `**` 加粗标记，并保持格式统一。信号词中英文对照, 术语英文放到括号内。只需要使用标记方式标记信号词即可, 无需出现“信号词”字眼，保持自然行文。
3. 自然地集中出现该段落内容主题独有的专有名词或术语，但不要过度堆砌，保持自然行文。
4. 使用任何能别出“章节边界”、并促使章节内部术语集中的标记方式分割长文档(默认为(markdown+mathjax+补充HTML片段(内联样式))作为回复格式, 否则按照用户指定格式回复), 使用明显的标题或分割符标记出章节边界，使得每个章节内部的块更加同质。
5. 对于上下文要额外注意, 由于注意力机制, 召回上下文时会召回紧密衔接的内容，上下文可能无法清晰切割, 因此需要注意用户问题的严格边界。
6. 每次回复需要加上唯一ID(格式: 回复ID: <最最重要的那个关键词,驼峰写法>-<YYYYMMDD日期>-<\d{3}自增长>), 方便后序引用(引用格式: `[inner: 回复ID]`)。

数学公式使用 mathjax 表达, 特殊token表达到markdown代码块中。

已知上下文:

- 本次只审查一个代码风格量表维度，不审查其他维度。
- 目标不是判断安全性或风格优劣，也不是偏好 Allman、K&R 或某种语言。
- 目标是判断“代码长什么样”：肉眼可见的 if/for/while 单语句体是否有大括号、是否 always-braces、是否混用。
- 需要警惕把大括号换行位置、缩进风格、语言风格优劣或 lint 强制误并入“单行控制流大括号使用”。
- 当前维度数据如下：

```json
{
  "id": "braceForSingleLine",
  "category": "formatting",
  "name": "单行控制流大括号使用 (Braces for Single-line Control Flow)",
  "descriptions": [
    "if、for后面直接跟一行短句，没有花括号，看起来简洁但随意",
    "只在紧跟多条语句时才出现花括号，单条语句时有时无",
    "即便只有一条语句也常能看到花括号，偶尔还能看到只有一行却用花括号包裹的情形",
    "所有if/for/while之后一定有一对花括号，哪怕里面只有一句，视觉上块边界很清晰",
    "屏幕上绝对找不到没有花括号的控制流体，每个块都完整包裹",
    "花括号不仅一定存在，而且左大括号绝不与控制流关键字在同一行，代码块呈现出非常整齐的分层形状"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“单行控制流大括号使用”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是“左大括号绝不与控制流关键字在同一行”是否属于另一个 brace style 维度。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把换行风格、缩进风格、lint 强制、风格优劣或语言偏好写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
