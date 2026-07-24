# 论文 PDF 说明

> 初次获取日期：2026-07-17；最近校验日期：2026-07-23。  
> 本目录收录主论文、直接前驱以及综述第 7 节引用的相关工作。

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

### 3/7. Sitarski（统一使用综述引用编号 [7]）

- 主文件：`07-sitarski-hats-hashed-array-trees.pdf`
- 兼容副本：`03-sitarski-hats-hashed-array-trees-web-archive.pdf`
- 标题：*Algorithm Alley: HATs: Hashed Array Trees*
- 作者：Edward Sitarski
- 出处：*Dr. Dobb's Journal of Software Tools*, 21(9), 1996, pp. 107-108
- 页数：6
- 来源：Internet Archive 保存的 Dr. Dobb's 原始文章页面打印版
- 存档地址：https://web.archive.org/web/20070930153913id_/http://www.ddj.com/architect/184409965?pgno=5
- SHA-256：`0ED0DF8D77969720D1639D04752F3D179B450E2D00A2A65B980EAD6440C0B248`

内容与用途：文章提出两级 HAT 结构，由 Top 索引块指向等长 Leaves 数据块。Top 和 Leaf 的大小均取 2 的幂，因此可用位移和掩码定位元素。文章给出顺序追加时的累计复制量、约 `2*sqrt(N)` 的最坏空间浪费以及早期性能实验，是综述解释 HAT 动机、结构和工程背景的直接来源。

版本与引用说明：公开检索没有找到该文章的出版社原生 PDF。两个本地文件均由同一 Internet Archive 页面打印生成，内容和 SHA-256 完全相同，并不是两篇不同论文。保留 `03-...` 仅用于兼容早期 P0 文件路径；新笔记、正文和参考文献一律使用 `07-...` 及引用编号 `[7]`。正式引用应按上述期刊文章信息著录，不能把 Internet Archive 打印件描述为另一篇论文或出版社 PDF。

### 4. Raman, Raman and Rao（综述引用编号 [8]）

- 文件：`08-raman-raman-rao-succinct-dynamic-data-structures.pdf`
- 标题：*Succinct Dynamic Data Structures*
- 作者：Rajeev Raman、Venkatesh Raman、S. Srinivasa Rao
- 出处：WADS 2001, LNCS 2125, pp. 426-437
- 页数：12
- 出版方版本：Springer 章节 PDF
- DOI：https://doi.org/10.1007/3-540-44634-6_39
- PDF 地址：https://link.springer.com/content/pdf/10.1007/3-540-44634-6_39.pdf
- SHA-256：`F73A07DCB719F7D6335AC3CEEE81529DE492AEEFF8F8AC15478617D5A1A0A503`

内容与用途：论文研究可搜索部分和、动态位向量以及允许任意位置插入和删除的动态数组。对动态数组，论文给出两种使用 `o(N)` 比特附加空间的结构：一种支持最坏 `O(1)` 访问和最坏 `O(N^epsilon)` 更新；另一种让所有操作达到摊还 `O(log N/log log N)`。它用于说明 Tarjan-Zwick 所处的简洁动态数据结构背景，同时也说明一般位置插删与仅在数组远端更新并非同一模型。

### 5. Raman and Rao（综述引用编号 [9]）

- 文件：`09-raman-rao-succinct-dynamic-dictionaries-and-trees.pdf`
- 标题：*Succinct Dynamic Dictionaries and Trees*
- 作者：Rajeev Raman、Satti Srinivasa Rao
- 出处：ICALP 2003, LNCS 2719, pp. 357-368
- 页数：12
- 出版方版本：Springer 章节 PDF
- DOI：https://doi.org/10.1007/3-540-45061-0_30
- PDF 地址：https://link.springer.com/content/pdf/10.1007/3-540-45061-0_30.pdf
- SHA-256：`F95B67EBDEF68CEE40A170DA737E28ADE4D8A780831A0E4034009A8E2FEF5501`

内容与用途：论文研究接近信息论最低空间的动态字典和动态二叉树。字典支持最坏常数时间成员查询与期望摊还常数时间更新；树表示在接近最低编码空间的同时支持常数时间导航和多对数级摊还更新。论文还讨论可扩展数组集合和内存分配模型，因此可作为“低阶冗余动态表示”的背景，但其字典和树结论不能直接作为 Tarjan-Zwick 可变长数组的复杂度结论。

### 6. Fredman and Saks（综述引用编号 [12]）

- 文件：`12-fredman-saks-the-cell-probe-complexity-of-dynamic-data-structures.pdf`
- 标题：*The Cell Probe Complexity of Dynamic Data Structures*
- 作者：Michael L. Fredman、Michael E. Saks
- 出处：STOC 1989, pp. 345-354
- 页数：10
- 出版方版本：ACM 会议论文 PDF
- DOI：https://doi.org/10.1145/73007.73040
- SHA-256：`637CF298D3F5387D03744A7B67BAD058C71E40B5D49D96D750339E0ECD01CB4E`

内容与用途：论文在 cell-probe 模型中研究 list representation、subset rank、partial sums 和 set union 等动态问题，并证明 list representation 与 subset rank 的摊还 `Omega(log N/log log N)` 下界。综述用它解释允许任意位置更新或维护秩信息时的复杂度障碍。该下界针对更强或不同的操作接口，不能直接解释为 Tarjan-Zwick 末端 `Grow/Shrink` 模型的下界。

### 7. Joannou and Raman（综述引用编号 [15]）

- 文件：`15-joannou-raman-an-empirical-evaluation-of-extendible-arrays.pdf`
- 标题：*An Empirical Evaluation of Extendible Arrays*
- 作者：Stelios Joannou、Rajeev Raman
- 出处：SEA 2011, LNCS 6630, pp. 447-458
- 页数：12
- 出版方版本：Springer 章节 PDF
- DOI：https://doi.org/10.1007/978-3-642-20662-7_38
- PDF 地址：https://link.springer.com/content/pdf/10.1007/978-3-642-20662-7_38.pdf
- SHA-256：`107F00A94B3658DA695232AF06F51005897EB3BB91EB8FC1583DBD903AA1DC52`

内容与用途：论文比较多种 extensible array 及 extensible-array collection 实现，测试增长、顺序访问和随机访问，并重点考察内部与外部内存碎片。它为综述中的实践讨论提供证据，说明渐近附加空间、访问速度、分配器行为和碎片化是不同评价维度。题名应为 *An Empirical Evaluation of Extendible Arrays*，不能写成此前误检索的 *Space-Efficient Dynamic Arrays*。

### 8. Katajainen（综述引用编号 [16]）

- 文件：`16-katajainen-worst-case-efficient-dynamic-arrays-in-practice.pdf`
- 标题：*Worst-Case-Efficient Dynamic Arrays in Practice*
- 作者：Jyrki Katajainen
- 出处：SEA 2016, LNCS 9685, pp. 167-183
- 页数：17
- 出版方版本：Springer 章节 PDF
- DOI：https://doi.org/10.1007/978-3-319-38851-9_12
- PDF 地址：https://link.springer.com/content/pdf/10.1007/978-3-319-38851-9_12.pdf
- SHA-256：`AD11B239A521E1C0981A73CF44CBE851F48ADCF4E5FDBE33A3DC7C7994E4C413`

内容与用途：论文实现并测试四类支持 `operator[]`、`push_back` 和 `pop_back` 最坏 `O(1)` 代价的动态数组方案，包括后台复制式可变长数组、分层分配结构、切片数组和分块结构。实验表明，具有最坏情况保证的实现通常慢于 C++ 标准库的摊还方案，而切片数组在论文的测试条件下构成较合理的实践折中。该结论依赖具体实现和实验环境，不能写成对所有平台的普遍性能结论。

## 校验方法

本目录共有九个 PDF 文件，对应八篇不同论文；其中两个 Sitarski 文件是同一存档的兼容副本。所有文件均已用 `pdfinfo`、`pdftotext` 和 SHA-256 检查：

- PDF 可以正常解析；
- 页数与预期一致；
- 首页或正文中可以抽取到正确标题和作者；
- Sitarski 存档版包含从文章引言到 References 的正文。
- 六份新增文件的正文与综述中的题名、作者和研究内容相符；
- 未把下载错误但章节编号相似的其他论文计入本目录。
