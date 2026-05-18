深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. dependency injection code style new concrete service constructor injection interface injection
2. dependency injection factory method service locator container annotation code appearance
3. constructor injection vs field injection @Inject @Autowired code review
4. dependency injection container configuration module provider binding code appearance
5. inversion of control dependency injection code structure visual indicators
6. manual wiring vs auto wiring dependency injection code appearance
7. whether full inversion of control no manual wiring is DI usage or framework architecture

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
- 目标不是判断架构质量，也不是偏好某个 DI 容器或框架。
- 目标是判断“代码长什么样”：肉眼可见的类内 new、工厂调用、ServiceLocator、构造函数参数、@Inject/@Autowired、声明式组件标记等形态。
- 需要警惕把完全控制反转、自动装配、框架成熟度、全局架构或测试性优劣误并入“依赖注入使用度”。
- 当前维度数据如下：

```json
{
  "id": "dependencyInjection",
  "category": "design",
  "name": "依赖注入使用度 (Dependency Injection Usage)",
  "descriptions": [
    "类方法体中可见 new ConcreteService()、ConcreteService.getInstance() 等直接获取依赖",
    "类内部调用 SomeFactory.create() 或 ServiceLocator.get()，依赖仍由当前类主动索取",
    "构造函数参数列表出现依赖对象，调用方以 new Client(service) 形式传入",
    "字段、构造器或 setter 上出现 @Inject/@Autowired，类内不再直接 new 或查找依赖",
    "构造器注入占主导，构造器签名集中列出依赖，参数多为接口或抽象类型",
    "该类文件只剩 @Component/@Inject/@Autowired 等声明式标记，无工厂调用或显式装配语句"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“依赖注入使用度”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是“完全控制反转”“看不到任何手动装配”“自动装配”是否偏离单文件代码外观。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把架构质量、框架成熟度、全局装配完整性、测试性优劣或框架偏好写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
6. 必须实际使用网页搜索，并在结果中列出至少 3 个公开资料来源或 citation；如果搜索不可用，必须明确说明无法完成本次审查。
