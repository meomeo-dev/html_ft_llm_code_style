深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. resource management code style close finally using with try-with-resources RAII
2. automatic resource management RAII smart pointer defer Drop AutoCloseable IDisposable
3. code appearance resource leaks open without close malloc without free
4. try finally close vs context manager with open code readability
5. AutoCloseable IDisposable resource management code patterns
6. smart pointers unique_ptr Arc resource management code appearance
7. whether defer Drop smart pointers are comparable automatic resource management scale

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
- 目标不是判断资源管理实际是否安全，也不是偏好某种语言机制。
- 目标是判断“代码长什么样”：肉眼可见的 open/close、try/finally、with/using、AutoCloseable/IDisposable、RAII、智能指针、defer、Drop 等形态。
- 需要警惕把内存安全、运行时行为、语言优劣或架构成熟度误并入“资源管理自动性”。
- 当前维度数据如下：

```json
{
  "id": "resourceManagement",
  "category": "performance",
  "name": "资源管理自动性 (Resource Management Automaticity)",
  "descriptions": [
    "f = open(...) 无对应 close()，malloc 无 free，原始文件描述符可见",
    "try: ... finally: f.close() 块可见，函数末尾有显式 dispose() 或 close() 调用",
    "with open(...) as f: 块结构，using (var conn = ...) 在 C# 中，整齐缩进的作用域块",
    "类有 __enter__/__exit__ 或 Dispose() 方法，implements AutoCloseable 可见",
    "每个资源持有类签名显示 AutoCloseable 或 IDisposable，@Cleanup 注解，try-with-resources 遍布",
    "无手动资源处理可见，智能指针（unique_ptr, Arc）占主导，defer 关键字或 Drop trait 在所有类型上实现"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“资源管理自动性”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是智能指针、Arc、defer、Drop 是否能与 with/using/AutoCloseable 放在同一外观轴上。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把内存安全、运行时正确性、语言优劣或架构成熟度写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
