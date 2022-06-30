## **Reduction**

![image-20220525160038794](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525160038794.png)

![image-20220525160531860](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525160531860.png)

合取范式的可满足性问题可以规约到停机问题【见上】。而所有的 NP 问题又可以规约可满足性问题，因此所有的 NP 问题可以规约到停机问题，停机问题就是一个 NP-hard 问题。

![image-20220525160538137](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525160538137.png)

![image-20220525161007592](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525161007592.png)

合取范式的可满足性问题是第一个被证明的 NP 完全问题，要证明所有的 NP 可以规约到一个问题是难度很大的，但在第一个 NP 完全问题被证明后，**要证明一个问题是 NP 完全的，只要证明①可满足性问题【或者其他NP完全问题】可以规约到这个问题，并且②这个问题是 NP 问题即可**

![image-20220525161747283](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525161747283.png)

### Satisfiability Problem

![image-20220525161946917](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525161946917.png)

**SAT** ：Boolean Satisfiability Problem **是NP 完全问题**，3-SAT 也是NP 完全问题

3-SAT 即指合取范式中的**一个子句即括号内的变量是最多 3 个**，如(a1∨a2∨z1)∧(z1∨a3∨z2)∧(z2∨a4∨z3)∧⋯∧(zl−3∨al−1∨al)

### Example 1: Max Clique Problem is NP-Complete

最大团问题/最大完全子图问题

![image-20220525162653706](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525162653706.png)

是 NP 问题

![image-20220525173253492](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525173253492.png)

每个子句都产生 3 个顶点，因此有 3k 个顶点，两个顶点之间有边当且仅当**①**它们不在同一个子句中**②**它们可以同时取真，不会相互矛盾，**即两个顶点不能分别是 x~i~ 和 x~i~ 取反**，其他情况都是可以同时取真的

![image-20220525174019707](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525174019707.png)

![image-20220525174730430](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525174730430.png)

![image-20220525174736811](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525174736811.png)

### Example 2: Dense Subgraph Problem is NP-Complete

![image-20220525180739932](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525180739932.png)

对于一个无向图 G，是否包含一个子图 H 有 K 个顶点和至少 Y 条边

容易想到，**最大团问题是这个问题的特例**【*特例是NP 完全，那么更通用的问题自然也是，只需要将通用问题中的可变参数设置为特例中的值即可*】，因此使用多项式规约，对于最大团问题的输入 G，K，转换成稠密子图问题的输入 G，K，Y=K(K-1)/2，而最大团问题是 NP 完全问题，因此稠密子图问题也是 NP 难问题，同时容易知道稠密子图问题是 NP 问题，因此是 NP 完全问题

### Example 3: Undirected Hamiltonian Cycle Problem is NP-Complete

**无向图**中的哈密尔顿回路问题

从**有向图的哈密尔顿回路问题【NP 完全】规约**

要将有向图变成无向图，直接去掉边的方向会丢失信息，不可行：

![image-20220525192930006](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525192930006.png)

1 个显然不行，2 个如下可以举出反例

![image-20220525182538911](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525182538911.png)

左边有向图是没有哈密尔顿回路的，但右边转换后的无向图是有的，因此右边有回路不能推断出左边有回路，即规约的第三条不满足

使用 3 个顶点来从有向图向无向图规约：

![image-20220525193046720](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525193046720.png)

![image-20220525182337865](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525182337865.png)

一定是有向边起点的 3 号点连接到终点的 1 号点

**从有向到无向，只要一个节点分离出来的节点数大于等于 3 即可**【*必须要要有一个中间节点 保证分离出的节点一起访问*】

**证明：**

1. 左边有 H 环->右边有 H 环：显然，在有向图中有 H 环，在对应的无向图中自然可以找到一样的环。
2. 左边有 H 环<-右边有 H 环：
   - 如果右边有 H 环，对于每个三元组的三个顶点，一定会被连续地遍历，否则比如在 v~1~ 不访问 v~2~ 而是去 z~3~，**那么 v~2~ 就再也不会被访问到了**，**因为 H 回路必须要回到起点**，如果之后通过访问 v~3~ 再访问到 v~2~ ，因为 v~2~ 只和 v~1~ 和 v~3~ 相连，那么会导致不能从 v~2~ 回到起点，不符合 H 环要访问到所有点的要求
   - 因为所有的三元组都会被连续地访问，因此如果存在 H 环，那么所有三元组的访问顺序一定是一样的，比如从 z~1~ 开始到 z~3~ 后接下来只能到下一个三元组的 1 号节点，如 y~1~，因此所有的三元组的访问顺序一样
   - 综合上面两个原因，三个点就可以收缩成 1 个点了，因为 3 个点都是连续访问的，所以就形成了原图 G 中的 H 环

