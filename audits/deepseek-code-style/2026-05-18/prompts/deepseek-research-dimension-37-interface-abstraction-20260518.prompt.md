深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. interface abstraction reliance code style concrete classes interfaces abstract classes code appearance
2. program to interface not implementation code review visual indicators
3. interface implementation pairs codebase file naming I prefix Impl suffix
4. over abstraction code smell too many interfaces abstract classes generics
5. public API through interfaces implementation hidden code appearance
6. interface inheritance hierarchy generic interfaces visual complexity
7. whether deep abstraction hierarchy is higher abstraction reliance or over abstraction different dimension

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
- 目标不是判断架构质量，也不是偏好 OOP 或某种语言。
- 目标是判断“代码长什么样”：肉眼可见的 concrete class、interface、abstract、接口/实现文件对、变量类型声明、公开 API 暴露形式、业务代码中的引用类型。
- 需要警惕把过度抽象、层次复杂度、架构优劣、封装质量或可测试性误并入“接口与抽象依赖程度”。
- 当前维度数据如下：

```json
{
  "id": "interfaceAbstraction",
  "category": "design",
  "name": "接口与抽象依赖程度 (Interface & Abstraction Reliance)",
  "descriptions": [
    "代码中只有具体类 class 的声明和使用，看不到 interface 或 abstract 关键词",
    "少量 interface 定义只出现在个别扩展点、回调或适配器附近",
    "多数主要服务存在接口/实现文件对，如 IXxx/XxxImpl 或 Xxx/XxxDefault",
    "方法参数、返回值和字段类型大多声明为接口或抽象类，而非具体类名",
    "公开 API 通过 interface 暴露，具体实现类只在内部包、私有类或装配处可见",
    "除对象构造和配置组装位置外，业务代码中的引用类型几乎都是接口或抽象类"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“接口与抽象依赖程度”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是“大量抽象类、多层接口继承、泛型接口”是否是更高依赖程度，还是过度抽象/复杂度维度。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把架构质量、过度抽象评价、封装质量、可测试性或语言偏好写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
6. 必须实际使用网页搜索，并在结果中列出至少 3 个公开资料来源或 citation；如果搜索不可用，必须明确说明无法完成本次审查。
