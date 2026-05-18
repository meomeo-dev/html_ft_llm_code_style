深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. type annotation strictness code appearance function parameters return types variables any generics
2. TypeScript strict mode noImplicitAny explicit any type annotations code style
3. Python type hints parameters return variables mypy strict code appearance
4. complex type expressions conditional types type assertions code readability
5. static typing strictness visible annotations no any code review
6. type annotation coverage variables functions signatures generic type density
7. whether complex conditional types are higher type strictness or type complexity dimension

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
- 目标不是判断类型系统质量，也不是偏好 TypeScript/Python/静态语言。
- 目标是判断“代码长什么样”：肉眼可见的参数类型、返回类型、变量类型、strict 标记、any、泛型尖括号、类型断言、复杂类型表达式。
- 需要警惕把复杂类型表达式、条件类型、类型体操、语言高级语法或类型系统能力误并入“类型注解严格度”。
- 当前维度数据如下：

```json
{
  "id": "typeAnnotation",
  "category": "naming",
  "name": "类型注解与静态类型严格度 (Type Annotation Strictness)",
  "descriptions": [
    "代码中完全看不到任何类型标注，变量、参数、返回值都是裸名",
    "只有函数定义的小括号内有类型标注，其它地方依然无类型",
    "所有函数签名都有类型标注，函数体内的变量依旧无类型",
    "文件顶部出现明显的严格模式标记，所有函数和变量定义处都带类型",
    "代码中看不到任何 any，每个标识符后都紧跟冒号和具体类型，泛型尖括号频繁出现",
    "整个文件被密集的类型信息包裹，复杂类型表达式、条件类型、类型断言遍布"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“类型注解与静态类型严格度”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是复杂类型表达式、条件类型、类型断言是否是更高严格度，还是类型复杂度/高级语法维度。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把类型系统质量、类型复杂度、语言高级语法、类型体操或静态语言偏好写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
