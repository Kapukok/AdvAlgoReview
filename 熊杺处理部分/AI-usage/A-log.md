# 成员 A 的 AI 使用记录

> 课程要求允许使用 AI 辅助理解和查询，但不接受 AI 代写。  
> 本日志应与版本历史一起保留，记录输入、输出用途、人工验证和最终是否采纳。  
> 不应删除旧记录；发现错误时追加更正。

## 记录模板

```markdown
## YYYY-MM-DD / 编号

- 使用工具：
- 使用目的：
- 输入摘要或对话链接：
- AI 生成内容：
- 人工核验材料：
- 发现的问题：
- 最终采纳、改写或放弃的内容：
```

## 2026-07-17

- 使用工具：OpenAI Codex。
- 使用目的：按照 `drafts/A-v0-revision-guide.md` 的顺序，初步更新 `drafts/A-background-and-lower-bound-v0.md`。
- 输入材料：修改指南、A 正文 v0、本地论文原文的原文内容，以及先前的证明阅读记录。
- 本轮修改范围：Theorem 4.1 的历史状态证明；Theorem 4.2 的模型假设、单调性和 Corollary 4.3；Sitarski HAT 的结构不变量、访问、更新、重建、空间分析和示例；Brodnik 两种变体的容量推导、更新、定位和 HAT 对比。
- 新增示例：HAT 的 `B=4,N=13` 文本图与 `i=10` 定位；Brodnik 递增块的 `N=8` 文本图与 `i=6` 定位。
- 关键纠正：Theorem 4.1 现在分别使用最终长度 `N`、历史长度 `N'`、块数 `k` 和大块容量 `ell`，并明确写出 `ell>sqrt(N)>=sqrt(N')`；Theorem 4.2 明确指出 `t` 的单调性只用于从 `t(N')` 过渡到 `t(N)`。
- 明确未处理：修改指南第五步以后的 geometric resizing 精确量化、动态内存引入增强、完整 related work、正式图形、引用键和原文页码。
- 人工核验要求：成员 A 应重新计算两个示例的下标；不看草稿口述两条下界；对照 Sitarski 与 Brodnik 原文补页码；把最终采用的段落改成自己的语言。
- 最终采纳情况：补充的部分经过人工审核内容后，删去了不符合原文描述的解释。

## 2026-07-17

- 使用工具：OpenAI Codex、公开网络检索、PowerShell 下载工具、Microsoft Edge 无头打印。
- 使用目的：获取 `sources/A-related-work.md` 中三篇 P0 文献的原文 PDF，并放入 `A-workspace/sources/papers/`。
- 获取结果：Tarjan-Zwick 使用项目已有 arXiv v2 PDF；Brodnik 等人使用 Robert Sedgewick 作者站点提供的 12 页 PDF；Sitarski 使用 Internet Archive 保存的 Dr. Dobb's 原始文章页面并打印成 6 页 PDF。
- 真实性说明：Sitarski 文件不是出版社原生 PDF，而是原始网页存档的 PDF 打印版；文件名和 `sources/papers/README.md` 已明确标注这一点。
- 验证方式：使用 `pdfinfo` 检查页数和 PDF 结构，使用 `pdftotext` 核对标题、作者与正文，并记录 SHA-256。
- 人工后续任务：成员 A 阅读 Brodnik 与 Sitarski 原文，补充正式稿中的原文页码；引用 Sitarski 时使用原刊书目信息。
- 最终采纳情况：三份文件已作为 P0 原文资料归档，正文中有关引用均引用自这三份文件

## 2026-07-18

- 使用工具：OpenAI Codex、本地 `pdftotext`。
- 使用目的：阅读已归档的 Sitarski 1996 与 Brodnik et al. 1999 P0 原文，单独总结它们相对 Tarjan-Zwick Sections 3-4 简述新增的内容。
- 输出文件：`sources/A-P0-original-papers-added-details.md`。
- Sitarski 提取重点：数据库案例、固定增量扩容的复制量、C/C++ 内存观察、Top/Leaves 位寻址、累计复制量约 `4N/3`、临时 leaf 例子、空间常数、边界优化、应用设想和早期基准。
- Brodnik 提取重点：randomized queue 动机、动态分配与 block-header 模型、`f(n)g(n)>=n` 下界、virtual superblocks、Grow/Shrink/Locate 算法、后台索引重建、buddy-system 版本、应用和双端结构。
- 风险与限制：Sitarski 基准平台较旧；网页存档 PDF 页码不等于原刊页码；原文中的实践主张不能自动推广到现代系统；摘要文档仍需成员 A 对照 PDF 核验。
- 最终采纳情况：作为 related-work 阅读笔记归档，经人工总结后已经并入 A 正文。
