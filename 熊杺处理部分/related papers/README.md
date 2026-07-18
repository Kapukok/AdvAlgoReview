# P0 原文 PDF 说明

> 获取与校验日期：2026-07-17。  
> 这些文件仍位于 `A-workspace` 暂存区，未移动到 `AdvAlgoReview`。

## 文件清单

### 1. Tarjan and Zwick

- 文件：`01-tarjan-zwick-optimal-resizable-arrays-arxiv-v2.pdf`
- 标题：*Optimal Resizable Arrays*
- 作者：Robert E. Tarjan、Uri Zwick
- 版本：arXiv:2211.11009v2，2023-05-29
- 页数：24
- 来源：项目中已有的 `06-optimal-resizable-arrays.pdf`
- 在线地址：https://arxiv.org/abs/2211.11009
- SHA-256：`DF5BFEF1740295B63131A1794F8628F8B6325918D29D9D079F3EE4315E4B4E41`

说明：这是当前中文翻译和页码记录所对应的 arXiv v2 原文。最终参考文献仍建议引用 2024 年 SIAM Journal on Computing 期刊版。

### 2. Brodnik et al.

- 文件：`02-brodnik-et-al-resizable-arrays-optimal-time-space.pdf`
- 标题：*Resizable Arrays in Optimal Time and Space*
- 作者：Andrej Brodnik、Svante Carlsson、Erik D. Demaine、J. Ian Munro、Robert Sedgewick
- 版本：WADS 1999 论文原文
- 页数：12
- 来源：Robert Sedgewick 作者站点
- 在线地址：https://sedgewick.io/wp-content/themes/sedgewick/papers/1999Optimal.pdf
- DOI：https://doi.org/10.1007/3-540-48447-7_4
- SHA-256：`2E91AAAC397FD175F1AFF6B94663DEBA03251FAC13C8D32C968033A31E572BC5`

另有 Luleå University of Technology 机构仓储记录：https://ltu.diva-portal.org/smash/record.jsf?pid=diva2%3A1000012

### 3. Sitarski

- 文件：`03-sitarski-hats-hashed-array-trees-web-archive.pdf`
- 标题：*HATs: Hashed Array Trees - Fast Variable-Length Arrays*
- 作者：Edward Sitarski
- 原始出处：Dr. Dobb's Journal，1996-09-01
- 页数：6
- 来源：Internet Archive 保存的 Dr. Dobb's 原始文章页面
- 存档地址：https://web.archive.org/web/20070930153913id_/http://www.ddj.com/architect/184409965?pgno=5
- SHA-256：`0ED0DF8D77969720D1639D04752F3D179B450E2D00A2A65B980EAD6440C0B248`

说明：公开检索没有找到该 1996 文章的出版社原生 PDF。本文件是把 Internet Archive 中保存的原始 Dr. Dobb's 文章页面直接打印为 PDF，正文包含文章标题、作者、完整论述和参考文献；页面同时保留了原网站导航及存档 URL。引用时仍应按期刊文章引用，而不是把本文件描述为出版社 PDF。

## 校验方法

三份文件均已用 `pdfinfo` 和 `pdftotext` 检查：

- PDF 可以正常解析；
- 页数与预期一致；
- 首页或正文中能抽取到正确标题和作者；
- Sitarski 存档版包含从文章引言到 References 的正文。
