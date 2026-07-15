Growth game: 

​	为了能够证明标准实现 grow 操作摊还成本的下界, 论文第 8 章提出了一个 growth game, 具体定义如下: 

​	对于 $(N,k,l)-$growth game, 给定三个非负整数 $N,k,l$, 其中: 

- $N$: 游戏结束前总共要插入的元素数量; 
- $k$: 可以使用的子数组数量; 
- $l$: 一个新建或合并后的子数组中允许预留的空位数量. 

​	游戏维护 $k$ 个子数组 $A_1,A_2,\dots,A_k$, 它们共同表示一个逻辑上的可变长数组 $A$. 为了简化后续的合并, 我们使元素倒序排列, 即 $A$ 最早的元素存放在 $A_k$ 中, 接下来的存在 $A_{k-1}$, 以此类推. 令$a_i=|A_i|$, 表示子数组 $A_i$ 中当前的元素数量. 

​	规定空的子数组必须在前面. 也就是说, $\forall i$ 使得 $a_i=0$, 对于 $\forall j,0<j<i$, 都有 $a_j=0$. 

​	规定只有第一个非空子数组可以有预留的空位. 也就是说, 如果 $A_i$ 是第一个非空子数组 (即它前面的所有子数组都是空数组 $\forall j,0<j<i,a_j=0$), 那么 $A_i$ 可以有至多 $l$ 个未使用的位置, 而 $A_{i+1},\dots,A_k$ 必须全部装满, 即 $\forall j,i<j\leq k$, $a_j$ 等于 $A_j$ 的容量. 因此, 整个数据结构中由于未填满而产生的空位最多就是 $l$. 

​	综上, 该数据结构所用的额外空间最多为 $k+l$. 

​	在 growth game 中, 忽略分配和释放所需的成本, 只考虑元素写入, 因此成本就是元素写入的次数. 每次 grow 操作加入一个新元素, 这有三种情况: 

1. 第一个非空子数组有空位
   那么就直接把新元素放进它的第一个空位, 操作成本显然为 $1$. 

2. 所有非空子数组都已经装满了, 但还有空的子数组
   那么就找到最后一个空子数组, 也就是编号最大的空子数组, 给它分配一个容量为 $l+1$ 的新子数组 (也就是最多可以预留的空位数量, 加上一个新元素的空间), 并把新元素放进它的第一个位置. 
   因为忽略内存分配的成本, 此处只写入了一个元素, 因此操作成本也是 $1$. 

   注意在前两种情况下, 玩家没有操作空间. 

3. 所有 $k$ 个子数组都已经装满了
   此时没有空子数组, 也没有预留空位. 需要玩家来选择一个整数 $i\in[k]$, 然后分配一个容量为 $(l+1)+\sum_{j=1}^ia_j$ (也就是最多可以预留的空位数量, 加上一个新元素的空间, 再加上前 $i$ 个子数组的元素总数), 然后把子数组 $A_i,A_{i-1},\dots,A_i$ 中的元素复制到新数组中, 复制时要保持逻辑数组的元素顺序. 接下来把新元素放入该数组的第一个空位, 此时新数组中刚好还剩下 $l$ 个空位. 最后释放旧的 $A_1,\dots,A_i$, 让新数组成为新的 $A_i$. 最后 $A_1,\dots,A_{i-1}$ 变为空, 而 $A_{i+1},\dots,A_k$ 保持不变. 
   操作成本为 $1+\sum_{j=1}^ia_j$, 即一个新元素的写入成本和所有被复制的旧元素的所需成本之和. 

​	Growth game 的目标是: 找到完成一个 $(N,k,l)-$growth game 的全部 $N$ 次插入所需要的最小总成本 $C_{N,k,l}$, 以及相应的摊还成本 $A_{N,k,l}=\frac{C_{N,k,l}}{N}$ , 和实现这个最小成本的最佳移动序列. 

​	如果一个真实数据结构有 $cN^{1/r}$ 的额外空间, 那么它可以对应一个 $k=cN^{1/r},l=cN^{1/r}$ 的 growth game. 实际上, growth game 是比真实数据结构更宽松的一个模型, 因为: 

- 玩家提前知道最终要插入的元素数量 $N$, 因此可以制定全局最优计划; 
- 真实数据结构的空间限制与其当前数组大小有关, 例如当数组有 $n$ 个元素时, 合理的额外空间限制是 $cn^{1/r}$, 而 growth game 允许在一开始就使用最大的 $cN^{1/r}$, 这使得 growth game 相比真实情况有更多可用的额外空间; 
- 真实数据结构增长时通常需要暂时同时保存旧内存块、新内存块以及其他辅助信息, 使其需要更大的额外空间, 但 growth game 忽略了内存分配成本. 

​	这些优势只会使 growth game 的最小成本更小, 比真实问题更容易, 所以 growth game 的最小成本可以充当真实数据结构最优解的一个下界. 



$l=0$: 

​	实际上, 空位的数量 $l$ 对降低平均成本没有帮助. 举例来说, 假设 $l=2$, 每次分配一个新的子数组后, 新的子数组内先放入一个新元素, 然后剩下 $2$ 个空位. 接下来两个新的元素只会依次填入这两个空位而没有玩家的操作空间. 

​	也就是说, 在玩家每次决策之后, 总会跟着 $l$ 次强制操作. 因此我们实际上可以把连续的 $l+1$ 次插入元素看作一次操作, 把这 $l+1$ 个元素捆绑为 $1$ 个元素. 如此, 元素写入所需的总成本缩小到了 $\frac{1}{l+1}$, 但元素数量也缩小到了 $\frac{1}{l+1}$, 因此平均成本不变, 即引理 8.2: 对于任意能被 $l+1$ 整除的 $N$,  $C_{N,k,l}=(l+1)C_{\frac{N}{k+1},k,0}$ 且 $A_{N,k,l}=A_{\frac{N}{k+1},k,0}$. 

​	这样一来, 我们就将 growth game $l>0$ 的情况规约为了 $l=0$ 的情况. 接下来主要研究 $l=0$ 的情况. 记 $C_{N,k}=C_{N,k,0},A_{N,k}=A_{N,k,0},(N,k)-$growth game$=(N,k,0)-$growth game. 



​	用向量 $\mathbf{a}=(a_1,a_2,\dots,a_k)\in\mathbb{N^k}$ 表示 $(N,k)-$growth game 的一个状态; 

​	定义 $P_{N,k}$ 为 $(N,k)-$growth game 所有合法的最终状态的集合, 即$P_{N,k}=\{\mathbf{a}|\sum_{i=1}^ka_i=N$ 且 $a_i=0\Rightarrow a_{i-1}=0,i=2,\dots,k\}$; 

​	对于 $\mathbf{a}\in P_{N,k}$, 定义 $C(\mathbf{a})=C_k(\mathbf{a})$ 为从状态 $(0,0,\dots,0)$ 到 状态 $\mathbf{a}$ 所需的最小成本, 显然 $C_{N,k}=\min_{\mathbf{a}\in P_{N,k}}C_k(\mathbf{a})$. 



​	 (引理 8.4) 接下来我们关注每个子数组的形成过程, 从而把总成本拆开分析: 

1. 假设最终状态是 $(a_1,a_2,\dots,a_{k-1},a_k)$, 考虑操作过程中, 最后一次改变 $A_k$ 的时刻. 改变 $A_k$ 要么是将新元素填入 $A_k$, 此时前面的子数组均为空; 要么是将 $A_1,\dots,A_k$ 合并为 $A_k$, 填入新元素并清空 $A_1,\dots,A_{k-1}$; 第一种情况实际上可以归纳为第二种情况. 因此, 这次操作结束后的状态一定是 $(0,0,\dots,0,a_k)$. 在此之后, $A_k$ 不再改变, 达到最终状态所需成本是建立前 $k-1$ 个子数组所需的成本 $C_{k-1}(a_1,\dots,a_{k-1})$. 
   由此可得递推式 $C_k(a_1,a_2,\dots,a_k)=C_k(0,\dots,0,a_k)+C_{k-1}(a_1,a_2,\dots,a_{k-1})$. 
2. 由上式归纳可得 $C_k(a_1,a_2,\dots,a_k)=\sum_{j=1}^kC_j(0,\dots,0,a_j)$. 
3. 考虑状态 $(0,\dots,0,a_k)$. 要达到这个状态所需的最后一步操作要求将此前已经存在的 $a_k-1$ 个元素合并到新块中, 并写入新元素, 因此最后这步操作的成本为 $a_k$; 而在这步之前, 要组织好已有的 $a_k-1$ 个元素所需的最低成本是 $C_{a_k-1,k}$. 
   因此$C_k(0,\dots,0,a_k)=C_{a_k-1,k}+a_k$. 
4.  综上, 对于 $\mathbf{a}\in P_{N,k}$, 如果有 $0=a_{i-1}<a_i$, 那么
   $C(\mathbf{a})=\sum_{j=i}^kC_j(0,\dots,0,a_j)=\sum_{j=i}^kC_{a_j-1,j}+a_j=N+\sum_{j=i}^kC_{a_j-1,j}$. 

​	由此我们把计算 $C(\mathbf{a})$ 拆成了计算若干个 $C_{N,k}$ 的子问题. 



定理 8.6: 

​	论文在定理 8.6 中给出了关于 $C_{N,k}$ 的以下命题: 

1. 如果对某个 $n\geq0$ 有 $\binom{n+k-1}{k}-1\leq N\leq\binom{n+k}{k}-1$, 那么 $C_{N,k}=(N+1)n-\binom{n+k}{k+1}$; 
2. 如果对某个 $n\geq1$ 有 $\binom{n+k-1}{k}\leq N<\binom{n+k}{k}$, 那么 $C_{N,k}-C_{N-1,k}=n$; 
3. 如果对某个 $n\geq0$ 有 $\binom{n+k-1}{k}-1\leq N<\binom{n+k}{k}-1$, 那么 $\forall i\in[k]$ 有  $C_{N,k}=C(\mathbf{a})\Leftrightarrow\binom{n+i-2}{i}\leq a_i\leq\binom{n+i-1}{i}$; 

​	可以通过数学归纳法证明以上定理. 为了证明以上定理, 我们需要以下命题:

​	 (引理 8.5) 

1. $\binom{n}{k}=\binom{n-1}{k-1}+\binom{n-1}{k}$
   这是一个众所周知的公式. 
2. $\sum_{i=0}^k\binom{n+i-1}{i}=\binom{n+k}{k}$
   可由以下归纳步骤证得: $\sum_{i=0}^k\binom{n+i-1}{i}=(\sum_{i=0}^{k-1}\binom{n+i-1}{i})+\binom{n+k-1}{k}=\binom{n+k-1}{k-1}+\binom{n+k-1}{k}=\binom{n+k}{k}$. 

​	 (命题 8.8) 当 $n=1$, 即 $0\leq N\leq k$ 时, $C_{N,k}=N$, 并且 $\forall\mathbf{a}\in P_{N,k}$, $C(\mathbf{a})=N$ 当且仅当 $\forall i\in[k],0\leq a_i\leq1$. 

​	 (命题 8.9) 假设定理 8.6(1) 对 $(N,k)$ 和 $(N-1,k)$ 都成立, 那么: 如果对某个 $n\geq1$ 有 $\binom{n+k-1}{k}\leq N<\binom{n+k}{k}$, 显然 $\binom{n+k-1}{k}-1<N\leq\binom{n+k}{k}-1$ 且 $\binom{n+k-1}{k}-1\leq N-1<\binom{n+k}{k}-1$. 应用定理 1, 可得 $C_{N,k}-C_{N-1,k}=((N+1)n-\binom{n+k}{k+1})-(Nn-\binom{n+k}{k+1})=n$. 也就是说, 当定理 8.6 (1) 对 $(N,k)$ 和 $(N-1,k)$ 都成立时, 定理 8.6 (2) 对 $(N,k)$ 成立. 

​	 (命题 8.10) 假设定理 8.6 (1) 对所有满足 $N'<N$ 且 $k'\leq k$ 的 $(N',k')$ 都成立, 那么取 $\mathbf{a}\in P_{N,k}$ 满足 $\forall i\in[k],\binom{n+i-2}{i}\leq a_i\leq\binom{n+i-1}{i}$, 则

​	$\begin{align}C(a)&=N+\sum_{i=1}^kC_{a_i-1,i} (引理 8.4) \\&=N+\sum_{i=1}^k(a_i(n-1)-\binom{n+i-1}{i+1}) (定理 8.6 (1)) \\&=N+N(n-1)-\sum_{i=1}^k\binom{n+i-1}{i+1}\\&=Nn-\sum_{i=1}^k\binom{n+i-1}{i+1}\\&=(N+1)n-(1+(n-1)+\sum_{i=1}^k\binom{n+i-1}{i+1})\\&=(N+1)n-(\binom{n-2}{0}+\binom{n-1}{1}+\sum_{j=2}^{k+1}\binom{n+j-2}{j})\\&=(N+1)n-\sum_{j=0}^{k+1}\binom{n+j-2}{j}\\&=(N+1)n-\sum_{j=0}^{k+1}\binom{(n-1)+j-1}{j}\\&=(N+1)n-\binom{(n-1)+(k+1)}{k+1} (引理 8.5) \\&=(N+1)n-\binom{n+k}{k+1}\end{align}$

​	综上, 当定理 8.6 (1) 对所有满足 $N'<N$ 且 $k'\leq k$ 的 $(N',k')$ 都成立时,  $\forall\mathbf{a}\in P_{N,k}$ 满足 $\forall i\in[k],\binom{n+i-2}{i}\leq a_i\leq\binom{n+i-1}{i}$, 有 $C(\mathbf{a})=(N+1)n-\binom{n+k}{k+1}$. 

​	 (命题 8.11) 考虑对某个 $n\geq1$ 有 $\binom{n+k-1}{k}-1\leq N<\binom{n+k}{k}-1$, 取 $\mathbf{a}\in P_{N,k}$, 那么: 

1. 假设 $\forall j\in[k],a_j\leq\binom{n+j-2}{j}$, 则
   $N=\sum_{j=1}^ka_j<\sum_{j=1}^k\binom{n+j-2}{j}=\sum_{j=0}^k\binom{(n-1)+j-1}{j}-1=\binom{n+k-1}{k}-1$ (引理 8.5), 
   与 $N\geq\binom{n+k-1}{k}-1$ 矛盾. 
   因此假设不成立, 如果 $\exists i\in[k]$ 使得 $a_i<\binom{n+i-2}{i}$, 那么一定 $\exists j\in[k]$ 使得 $a_j>\binom{n+j-2}{j}$. 
2. 类似地, 假设 $\forall i\in[k],a_i\geq\binom{n+i-1}{i}$, 则
   $N=\sum_{i=1}^ka_i>\sum_{i=1}^k\binom{n+i-1}{i}=\sum_{i=0}^k\binom{n+i-1}{i}-1=\binom{n+k}{k}-1$ (引理 8.5), 
   与 $N\leq\binom{n+k}{k}-1$ 矛盾. 
   因此假设不成立, 如果 $\exists j\in[k]$ 使得 $a_j>\binom{n+j-1}{j}$, 那么一定 $\exists i\in[k]$ 使得 $a_i<\binom{n+i-1}{i}$. 

​	 (命题 8.12) 假设定理 8.6 (2) 对所有满足 $N'<N$ 且 $k'\leq k$ 的 $(N',k')$ 都成立, 并且对某个 $n\geq1$ 有 $\binom{n+k-1}{k}-1\leq N\leq\binom{n+k}{k}-1$, 取 $\mathbf{a}\in P_{N,k}$, 但不满足 $\forall i\in[k],\binom{n+i-2}{i}\leq a_i\leq\binom{n+i-1}{i}$: 

1. 如果 $\exists i\in[k]$ 使得 $a_i<\binom{n+i-2}{i}$, 根据命题 8.11 (1),  $\exists j\in[k]$ 使得 $a_j>\binom{n+j-2}{j}$. 取 $\mathbf{b}=(b_1,b_2,\dots,b_k)\in P_{N,k}$, 其中 $b_i=a_i+1,b_j=a_j-1,\forall l\in[k]\backslash\{i,j\}$. 根据定理 8.6 (2), 有$C_{a_i,i}-C_{a_i-1,i}\leq n-2$ 且 $C_{a_j-1,j}-C_{a_j-2,j}\geq n-1$. 因此
   
   $\begin{align}C(\mathbf{b})-C(\mathbf{a})&=N+\sum_{l:b_l>0}C_{b_l-1,l}-N-\sum_{l:a_l>0}C_{a_l-1,l} (引理 8.4)\\&=C_{b_i-1,i}+C_{b_j-1,j}-C_{a_i-1,i}-C_{a_j-1,j}\\&=C_{a_i,i}+C_{a_j-2,j}-C_{a_i-1,i}-C_{a_j-1,j}\\&=(C_{a_i,i}-C_{a_i-1,i})-(C_{a_j-1,j}-C_{a_j-2,j})\\&<0\end{align}$
2. 如果 $\exists j\in[k]$ 使得 $a_j<\binom{n+j-1}{j}$, 根据命题 8.11 (1),  $\exists i\in[k]$ 使得 $a_i>\binom{n+i-1}{i}$. 取 $\mathbf{b}=(b_1,b_2,\dots,b_k)\in P_{N,k}$, 其中 $b_i=a_i+1,b_j=a_j-1,\forall l\in[k]\backslash\{i,j\}$. 根据定理 8.6 (2), 有$C_{a_i,i}-C_{a_i-1,i}\leq n-1$ 且 $C_{a_j-1,j}-C_{a_j-2,j}\geq n$. 因此
   
   $\begin{align}C(\mathbf{b})-C(\mathbf{a})&=N+\sum_{l:b_l>0}C_{b_l-1,l}-N-\sum_{l:a_l>0}C_{a_l-1,l}(引理 8.4)\\&=C_{b_i-1,i}+C_{b_j-1,j}-C_{a_i-1,i}-C_{a_j-1,j}\\&=C_{a_i,i}+C_{a_j-2,j}-C_{a_i-1,i}-C_{a_j-1,j}\\&=(C_{a_i,i}-C_{a_i-1,i})-(C_{a_j-1,j}-C_{a_j-2,j})\\&<0\end{align}$

​	因此如果定理 8.6 (2) 对所有满足 $N'<N$ 且 $k'\leq k$ 的 $(N',k')$ 都成立, 并且对某个 $n\geq1$ 有 $\binom{n+k-1}{k}-1\leq N\leq\binom{n+k}{k}-1$, 取 $\mathbf{a}\in P_{N,k}$, 但不满足 $\forall i\in[k],\binom{n+i-2}{i}\leq a_i\leq\binom{n+i-1}{i}$, 那么一定存在 $\mathbf{b}$ 满足 $C(\mathbf{a})>C(\mathbf{b})$, 所以$C(\mathbf{a})>C_{N,k}$, 即 $\mathbf{a}$ 一定不是一个最优的最终状态. 



​	现在我们终于可以证明定理 8.6 了. 

​	Basis: 由命题 8.8 可知, 定理在 $0\leq N\leq k$ 时成立.
​	Induction: 我们需要证明如果定理对所有满足 $N'<N$ 且 $k'\leq k$ 的 $(N',k')$ 都成立, 那么对 $(N,k)$ 也成立. 由命题 8.10 可知, 所有满足 $\forall i\in[k],\binom{n+i-2}{i}\leq a_i\leq\binom{n+i-1}{i}$ 的 $\mathbf{a}\in P_{N,k}$ 都有 $C(\mathbf{a})=(N+1)n-\binom{n+k}{k+1}$, 同时由命题 8.12 可知不满足上述条件的 $\mathbf{a}$ 一定不是一个最优的最终状态, 所以最小成本 $C_{N,k}$ 就是 $(N+1)n-\binom{n+k}{k+1}$. 定理 8.6 的 (1) (3) 得证. 又由命题8.9可知 (2) 成立. 

​	定理 8.6 得证. 

​	由定理 8.6, 我们可以得到以下推论: 

​	 (推论 8.13)

1. 如果 $N=\binom{n+k}{k}-1$, 那么根据定理 8.6 (1), $C_{N,k}=(N+1)n-\binom{n+k}{k+1}=\binom{n+k}{k}n-\binom{n+k}{k+1}=\binom{n+k}{k}n-\frac{n}{k+1}\binom{n+k}{k}=\frac{kn}{k+1}\binom{n+k}{k}=\frac{kn}{k+1}(N+1)$
2. 如果 $N=\binom{n+k-1}{k}$, 那么 $C_{N,k}>C_{N-1,k}=\frac{k(n-1)}{k+1}N$ 
   如果 $\binom{n+k-1}{k}< N\leq\binom{n+k}{k}-1$, 那么根据定理 8.6 (2), $C_{N,k}=C_{N-1,k}+n\geq\frac{k(n-1)}{k+1}(N-1)+n\geq\frac{k}{k+1}(n-1)N$. 因此 $A_{N,k}\geq\frac{k}{k+1}(n-1)\geq\frac{1}{2}(n-1)$