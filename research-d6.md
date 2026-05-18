深度搜索, 逐步的, 每步搜索一个查询:
1. 搜索主流风格指南中关于函数/方法命名长度与信息量的规范
2. 搜索函数名称长度与代码视觉扫描效率的关系
3. 搜索命名详细度作为代码风格光谱维度的设计

已知上下文: 代码风格调优器，仅关心代码视觉外观，0-5量表

任务:
审查维度"函数/方法命名详细度 (Function/Method Naming Verbosity)":

0: 仅使用单个通用动词或字母，无目标信息（如 do, run, f）
1: 动词与名词均采用缩写形式，视觉紧凑（如 calcTotal, getVal, initCfg）
2: 动词完整拼写，名词为泛化词，未揭示业务含义（如 calculateTotal, processData, fetchInfo）
3: 动词完整拼写，名词具有明确业务含义，不含缩写（如 calculateRevenue, fetchUserList, updateOrderStatus）
4: 在明确动作与目标基础上，增加最小必要上下文（如 calculateRevenueForYear, fetchUserById）
5: 名称包含多个动作或多余细节，视觉长度显著超出常规（如 calculateRevenueAndApplyDiscounts, fetchUserAndUpdateCache）

审查：0-5是否形成严格度递增？5级作为"过度详细"封顶是否合理？描述聚焦视觉外观？有问题给完整 descriptions。
