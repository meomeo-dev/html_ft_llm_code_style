深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. code readability algorithmic complexity comments Big O code review
2. algorithm efficiency focus code style nested loops Big O annotations
3. benchmarks directory performance tests codebase convention
4. documenting time complexity space complexity in docstrings
5. algorithm library imports heap deque Dijkstra quicksort code appearance
6. code smell nested loops algorithmic complexity performance
7. whether benchmark files and analysis markdown are algorithmic efficiency code style

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
- 目标不是判断算法实际性能，也不是偏好某种语言或算法库。
- 目标是判断“代码长什么样”：肉眼可见的循环形态、复杂度注释、数据结构/算法命名、复杂度 docstring 或递推推导注释。
- 需要警惕把真实性能、正确性、文档成熟度、测试覆盖或工程流程误并入“算法效率关注度”。
- 当前维度数据如下：

```json
{
  "id": "algorithmicEfficiency",
  "category": "performance",
  "name": "算法效率关注度 (Algorithmic Efficiency Focus)",
  "descriptions": [
    "三层以上缩进的 for/while 嵌套循环可见，注释无 Big-O 或复杂度字样",
    "深层嵌套减少到两层以内，重构块上方出现 O(n^2) -> O(n log n) 对比注释",
    "break、continue 或提前 return 可见，热点循环旁标注 Time O(n) 等简短复杂度",
    "导入 deque、heapq 等数据结构，注释或变量名引用 Dijkstra、merge_sort 等算法名",
    "函数 docstring 首行固定写 Complexity: Time O(...), Space O(...)",
    "代码块上方包含递推关系推导，如 T(n) = 2T(n/2) + O(n) -> O(n log n)"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“算法效率关注度”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是具体算法名称、数据结构导入、break/continue 是否偏离“代码长什么样”。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把真实性能、性能测试成熟度、文档成熟度、正确性或算法优劣写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
