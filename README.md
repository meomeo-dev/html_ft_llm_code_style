# AI 代码风格调优器

交互式代码写法画像调节器，通过 50 个维度和 7 个预设生成可复制的
代码风格提示词。

- 在线预览（GitHub Pages）: https://meomeo-dev.github.io/html_ft_llm_code_style/
- 仓库地址: https://github.com/meomeo-dev/html_ft_llm_code_style

## 功能

- 50 个代码写法维度：覆盖格式、命名、注释、结构、运行标记和测试写法。
- 7 个角色预设：代码规范负责人、业务线主力、赶 Demo 的同事、
  公共库维护者、平台组老员工、重构老手、技术文档作者。
- 实时生成提示词：滑块调整后立即输出连续文本提示词。
- 本地可用：单个 `index.html` 即可离线打开。

## 使用

- 在线使用: 打开 Pages 链接。
- 本地使用: 克隆仓库后直接打开 `index.html`。

```bash
git clone https://github.com/meomeo-dev/html_ft_llm_code_style.git
cd html_ft_llm_code_style
open index.html
```

## 部署

本仓库通过 GitHub Actions 发布到 GitHub Pages。

- 推送到 `main` 分支会触发部署。
- 部署产物只包含单页面 `index.html`。
- 当前访问地址为
  `https://meomeo-dev.github.io/html_ft_llm_code_style/`。

## 许可协议

MIT
