深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. code reusability code duplication extract function common util module code appearance
2. DRY principle duplicated code code smell visual indicators
3. duplicated code detection static analysis CPD jscpd code review
4. shared library internal util package code reuse visual structure
5. code reuse enforcement static checker annotation DRY code appearance
6. duplicated blocks refactoring extract method common module code style
7. whether static analysis enforcement belongs to code reusability code appearance

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
- 目标不是判断复用设计质量，也不是偏好公共库或工具。
- 目标是判断“代码长什么样”：肉眼可见的重复块、抽取函数调用、common/util import、lib 目录、重复检测注释或工具标记。
- 需要警惕把静态检查强制、流程治理、架构成熟度、DRY 教条或“任何重复不可见”绝对化误并入“代码复用强制力”。
- 当前维度数据如下：

```json
{
  "id": "codeReusability",
  "category": "design",
  "name": "代码复用强制力 (Code Reusability Enforcement)",
  "descriptions": [
    "屏幕上出现大段完全相同的代码块，复制粘贴痕迹明显，无函数提取",
    "已有两次重复代码块但仍未提取，视觉上能看到相同逻辑在多处出现",
    "重复逻辑被提取为独立函数，原位置替换为函数调用，屏幕上出现清晰的抽取后单行调用",
    "所有重复代码均迁移至公共模块，屏幕上的业务文件简洁，大量 import 来自 common、util 等包",
    "项目中构建了内部库/工具集，屏幕可见统一的 lib 目录，复用以引入库的形式出现",
    "任何重复都不可见，静态检查工具注解提示 DRY 严格执行，每一段逻辑只出现一次"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“代码复用强制力”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是静态检查强制、任何重复不可见、每段逻辑只出现一次是否偏离代码外观。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把流程治理、架构成熟度、设计质量、DRY 教条或绝对化无重复写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
