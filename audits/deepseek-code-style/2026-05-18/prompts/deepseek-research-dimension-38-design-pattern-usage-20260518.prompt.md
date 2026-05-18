深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. design patterns code appearance Factory Adapter Proxy Strategy Observer Decorator class names
2. GoF design patterns code review visual indicators class naming
3. pattern overuse anti pattern code smell design pattern abuse
4. singleton factory strategy observer decorator implementation code structure
5. design pattern application level code style pattern names suffixes
6. pattern language codebase visual structure modules class diagrams
7. whether forced design pattern usage is higher pattern application or negative overuse dimension

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
- 目标不是判断设计质量，也不是偏好 GoF、OOP 或某种架构。
- 目标是判断“代码长什么样”：肉眼可见的 Singleton/getInstance、Factory、Adapter、Proxy、Strategy、Observer、Decorator、类名后缀、模式目录/类结构。
- 需要警惕把模式滥用、强制套用、架构优劣、设计成熟度或过度工程化误并入“设计模式应用程度”。
- 当前维度数据如下：

```json
{
  "id": "designPatternUsage",
  "category": "design",
  "name": "设计模式应用程度 (Design Pattern Application Level)",
  "descriptions": [
    "屏幕上看到长过程式函数，无任何可识别的模式结构，视觉上像一连串平铺的指令",
    "零星出现 Singleton 类的 getInstance() 或简单工厂方法，视觉上能识别出个别典型模式签名",
    "根据场景散布 Observer、Strategy、Decorator 等结构，模式类名时有出现但不密集",
    "代码中积极使用 GoF 模式，类名带 Factory、Adapter、Proxy 后缀非常频繁",
    "模式成为主要设计语言，几乎每个模块都按某模式组织，屏幕上类图感强烈",
    "强制套用经典模式，每个问题域都对应一个模式，视觉上到处是标准模式样板"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“设计模式应用程度”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是“强制套用经典模式”“每个问题域都对应一个模式”是否是应用程度，还是模式滥用/设计质量维度。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把设计质量、模式滥用评价、过度工程化、架构成熟度或语言偏好写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
