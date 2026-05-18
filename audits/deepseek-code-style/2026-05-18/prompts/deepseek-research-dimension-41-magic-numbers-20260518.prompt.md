深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. magic numbers strings code smell named constants zero one exceptions
2. avoid magic numbers code style named constants literal 0 1
3. magic strings constants enum code readability visual indicators
4. no magic numbers static analysis ignore 0 1 -1 code review
5. named constants all caps readability overuse ZERO ONE anti pattern
6. hard coded strings constants configuration code appearance
7. whether replacing 0 and 1 with ZERO ONE is higher quality or over abstraction

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
- 目标不是判断可读性质量，也不是执行某个 lint 规则。
- 目标是判断“代码长什么样”：肉眼可见的裸数字/字符串、文件顶部常量、ALL_CAPS 常量、枚举、命名常量密度、0/1 是否裸露。
- 需要警惕把 ZERO/ONE 常量化、过度抽象、lint 规则、质量评价或语言风格偏好误并入“魔法数字/字符串使用度”。
- 当前维度数据如下：

```json
{
  "id": "magicNumbers",
  "category": "readability",
  "name": "魔法数字/字符串使用度 (Magic Numbers/Strings Usage)",
  "descriptions": [
    "屏幕上数字和字符串直接写在表达式里，代码逻辑与具体数值混杂在一起",
    "偶尔几个重复出现的相同数值被提出来放到文件顶部的命名常量里",
    "代码中凡是能看出业务含义的数字都变成了大写的英文常量名，0和1仍直接出现",
    "几乎看不到裸露的数字，除了循环变量的步进值0和1，其它全是带下划线的大写常量",
    "表达式里看不到任何直接写死的数字，所有数值都有一个名字",
    "连0和1都成了ZERO、ONE之类的大写常量，整个文件没有任何数字字面量直接裸露"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“魔法数字/字符串使用度”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进；注意名称是“使用度”，但描述似乎从多到少。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是 ZERO/ONE 是否是更高等级，还是过度抽象/可读性反向。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把质量评价、lint 强制、过度抽象、语言风格偏好或绝对零字面量写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
