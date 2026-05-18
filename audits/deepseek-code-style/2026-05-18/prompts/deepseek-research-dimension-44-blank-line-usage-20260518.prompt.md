深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. blank line usage code style function separation logical sections
2. blank lines formatting style guide between functions classes methods code appearance
3. PEP8 blank lines top level functions methods logical sections
4. Google style guide blank lines code readability
5. formatter blank lines preserve remove multiple blank lines code style
6. excessive blank lines code smell formatting visual grouping
7. whether exact blank line distance every element is formatting strictness or over specification

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
- 目标不是判断可读性质量，也不是偏好某个 formatter。
- 目标是判断“代码长什么样”：肉眼可见的空行数量、函数/类之间空行、逻辑段落分组、空行一致性、多空行。
- 需要警惕把自动格式工具、绝对像素/印刷品规整、过度规范、格式化流程或风格优劣误并入“空行使用规范”。
- 当前维度数据如下：

```json
{
  "id": "blankLineUsage",
  "category": "formatting",
  "name": "空行使用规范 (Blank Line Usage)",
  "descriptions": [
    "代码段之间空行数量不一，有的粘连、有的空多行，整体没有可见规律",
    "函数或类等顶层定义之间有空行，但函数内部逻辑块经常粘连",
    "逻辑段落之间使用空行分组，但一行、两行或多行的数量还不统一",
    "类、函数和主要逻辑段前后的空行数量遵循固定约定，布局可预期",
    "全文件类似元素之间的空行数量高度一致，视觉节奏稳定且少有突变",
    "空行只出现在预期的结构边界和逻辑组之间，多余空行与粘连块都很少见"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“空行使用规范”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是自动格式化工具、任何两个元素距离精确、印刷品般规整是否偏离空行外观。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把 formatter 流程、过度规范、可读性质量、风格优劣或绝对精确写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
6. 必须实际使用网页搜索，并在结果中列出至少 3 个公开资料来源或 citation；如果搜索不可用，必须明确说明无法完成本次审查。
