深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. comparison operand ordering code style yoda conditions constant left variable right
2. Yoda conditions code style variable constant comparison readability
3. ESLint yoda rule always never exceptRange code appearance
4. comparison ordering consistency constants left right code review
5. yoda conditions anti pattern or style preference code appearance
6. null == variable vs variable == null comparison operand order
7. whether variable-left and yoda are monotonic levels or style alternatives

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
- 目标不是判断可读性质量，也不是偏好 Yoda 或非 Yoda 写法。
- 目标是判断“代码长什么样”：肉眼可见的比较表达式中变量、常量、null、字面量位于运算符哪一侧，以及这种方向是否一致。
- 需要警惕把 Yoda 条件当作更高等级、工具强制、错误标记、可读性优劣或语言安全性误并入“比较操作数顺序”。
- 当前维度数据如下：

```json
{
  "id": "comparisonOrdering",
  "category": "readability",
  "name": "比较操作数顺序 (Comparison Operand Ordering)",
  "descriptions": [
    "比较表达式左右位置随意，变量和常量可能出现在==任意一侧",
    "绝大多数比较中，常量出现在运算符右侧，偶尔有一两处例外但不显眼",
    "所有比较中，常量始终在右侧，变量在左侧，看上去自然易读",
    "常量被放在左侧，变量在右侧，比如if(null==x)这样的倒装写法贯穿全文",
    "涉及相等性判断时，常量统统在左，形成非常刻意的Yoda风格视觉印记",
    "整个文件中比较的方向完全一致，并且工具强制，任何不一致都会导致视觉标记"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“比较操作数顺序”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是变量左/常量右与 Yoda 常量左是否是风格替代而非递进等级，以及工具强制/视觉标记是否越界。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把工具强制、错误标记、可读性质量、语言安全性或 Yoda/非 Yoda 优劣写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
