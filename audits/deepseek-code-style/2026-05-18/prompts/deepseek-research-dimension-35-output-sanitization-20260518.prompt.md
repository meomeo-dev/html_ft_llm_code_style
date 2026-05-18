深度搜索, 逐步的, 每步搜索一个查询, 逐步串行地从互联网中搜索收集所需的多个维度信息:
1. output encoding sanitization code style HTML escaping JavaScript escaping URL encoding
2. OWASP output encoding contexts escapeHtml escapeJs encodeURIComponent
3. template auto escaping code appearance output sanitization
4. Content Security Policy vs output encoding sanitization difference
5. centralized output encoding helper safe HTML wrapper code appearance
6. string concatenation user input HTML XSS code review output encoding
7. whether CSP and middleware belong to output sanitization code appearance scale

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
- 目标不是判断真实 XSS 防护有效性，也不是偏好某个模板引擎。
- 目标是判断“代码长什么样”：肉眼可见的裸拼接、escape/encode 函数、上下文编码、模板自动转义标记、集中安全输出 helper。
- 需要警惕把 CSP 响应头、安全策略、真实漏洞防护、架构层数或中间件治理误并入“输出清理”。
- 当前维度数据如下：

```json
{
  "id": "outputSanitization",
  "category": "concurrencySecurity",
  "name": "输出清理 (Output Sanitization)",
  "descriptions": [
    "屏幕上是字符串拼接，没有任何转义函数，视觉上用户数据直接嵌入 HTML",
    "出现 htmlEscape() 等基本转义调用，视觉上输出语句会包裹一层简短函数",
    "根据输出上下文分别可见 escapeHtml()、escapeJs()、encodeURIComponent() 等编码函数",
    "模板文件视觉上使用自动转义语法，转义由引擎隐式完成，不再显式调用函数",
    "输出代码旁边可见 Content-Security-Policy 头设置语句，配合转义函数共同出现",
    "所有输出都通过统一的安全函数/中间件，屏幕上不会有任何直接的拼接或裸变量输出"
  ]
}
```

任务:

请只审查这个维度：

1. 判断维度名称是否准确表达“输出清理/输出编码”的代码外观。
2. 判断 0-5 档是否在同一条视觉维度上单调递进。
3. 找出是否存在不必要、误导或跨维度的内容，尤其是 Content-Security-Policy、统一中间件、所有输出是否偏离单文件代码外观。
4. 若需要修改，给出 6 条替代文案，要求每条都能从代码外观直接观察，避免把 CSP、安全策略、真实防护效果、架构层数或框架偏好写进量表。
5. 明确说明哪些建议是基于公开资料，哪些只是你的推断。
