# `msb` 相关资料截图索引

这些截图用于核对 `review.md` §9.7.3 中的表述：

> Fredman–Willard 的方法使用乘法；不使用乘法时，Brodal 的方法需要 $\mathrm{O}(\log\log w)$；Brodnik、Miltersen 和 Munro 给出了相匹配的下界。

## 1. 最直接的引用入口

- [Tarjan–Zwick，第 1368 页](Tarjan-Zwick_p1368_msb引用总览.png)

这一页第一段直接概括了三项结论，并给出原文参考文献编号 `[7]`、`[13]` 和 `[3]`。如果正文只想先补一个最直接的页码引用，可以写成 `[1, p. 1368]`。

## 2. 允许乘法时的常数时间算法

- [Fredman–Willard，第 431 页](Fredman-Willard_p431_msb常数时间算法.png)
- [Fredman–Willard，第 432 页](Fredman-Willard_p432_msb常数时间算法.png)

第 431 页开始定义并构造 `msb(u,v)` 的常数时间计算，第 432 页完成两阶段算法。其位压缩和定位步骤使用乘法。

文献信息：

> M. L. Fredman and D. E. Willard, “Surpassing the Information Theoretic Bound with Fusion Trees,” *Journal of Computer and System Sciences*, 47(3), 1993, pp. 424–436. DOI: 10.1016/0022-0000(93)90040-4.

## 3. 不使用乘法时的 $\mathrm{O}(\log\log w)$ 算法

- [Brodnik–Miltersen–Munro，BRICS 报告第 7 页](Brodnik-Miltersen-Munro_BRICS-p7_loglog算法.png)
- [Brodnik–Miltersen–Munro，BRICS 报告第 8 页](Brodnik-Miltersen-Munro_BRICS-p8_Brodal说明.png)

第 7–8 页给出 `RightmostOne` 的 $\mathrm{O}(\log\log w)$ 算法。第 8 页末尾明确说明，Gerth Brodal 指出稍加修改即可用同一思路寻找最高有效置位。

第 6 页的[弱非一致性背景](Brodnik-Miltersen-Munro_BRICS-p6_弱非一致性背景.png)也一并保留，供需要交代机器模型和预计算常数时使用。

## 4. 匹配下界

- [Brodnik–Miltersen–Munro，BRICS 报告第 12 页](Brodnik-Miltersen-Munro_BRICS-p12_匹配下界背景.png)
- [Brodnik–Miltersen–Munro，BRICS 报告第 13 页](Brodnik-Miltersen-Munro_BRICS-p13_匹配下界定理与证明.png)
- [Brodnik–Miltersen–Munro，BRICS 报告第 14 页](Brodnik-Miltersen-Munro_BRICS-p14_匹配下界证明.png)

第 13 页的 Theorem 15 明确给出：在不含乘法的基本指令集下，寻找一个机器字最左或最右的置位需要 $\Omega(\log\log w)$ 时间；第 13–14 页给出证明。因此它与第 7–8 页的 $\mathrm{O}(\log\log w)$ 算法匹配。

文献信息：

> A. Brodnik, P. B. Miltersen, and J. I. Munro, “Trans-Dichotomous Algorithms without Multiplication—Some Upper and Lower Bounds,” *Proceedings of WADS 1997*, LNCS 1272, pp. 426–439. DOI: 10.1007/3-540-63307-3_80.

## 建议的正文引用方式

如果只想简洁补证据，可以把 §9.7.3 的引用写成：

> Fredman–Willard 的方法使用乘法并在常数时间内计算 `msb`；不使用乘法时，Brodal 的方法需要 $\mathrm{O}(\log\log w)$；Brodnik、Miltersen 和 Munro 给出了相匹配的下界 `[1, p. 1368]`。

若希望引用到原始工作，则再分别加入 Fredman–Willard 和 Brodnik–Miltersen–Munro 两条参考文献。
