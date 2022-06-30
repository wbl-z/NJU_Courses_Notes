# 25 Tutorial

![image-20220518140220761](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518140220761.png)

## Longest increasing subsequences

![image-20220518140439904](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518140439904.png)

![image-20220518141305821](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518141305821.png)

把子问题划分成**以 a~i~ 结尾的增长子序列**

根据条件构建边，即形成一个 DAG

从头开始看最长增长子序列，后面的是指向这个顶点的顶点的 length + 1，1即为该顶点

![image-20220518141546902](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518141546902.png)

> 另外做法：【一般有很多种子问题划分方式】【自顶向下方法】
>
> 类似前面的课程，将问题划分成 p(n)，n个元素中的最长增长子序列，规模即子问题个数同样是n
>
> p(n) = max{p(n-1), p(n~i~-1)}如果这个最长增长子序列不包含 n，那么规模直接降到 n-1；如果包含 n，那么就往前找到第一个比 n 小的 n~i~ 【不可能是 n~i~ 和 n 中间的节点，因为中间的节点和 n 不会构成增长序列】

**:star:注意：自顶向下方法要做备忘字典，自下向上方法要存储好已经计算出的值**

**核心就是利用小规模问题的答案构造出大问题的答案**

**DP 事实上就是递归，只是把递归中会出现的重复计算通过备忘或合理安排顺序来消除**

![image-20220518142333364](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518142333364.png)

## Longest-Common-Subsequence Problem

最长公共子序列——二维动态规划问题

![image-20220518142808502](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518142808502.png)

### How to define a subproblem?

![image-20220518144822374](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518144822374.png)

### How to use the small solutions to solve large problem?

![image-20220518145237699](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518145237699.png)

用一个二维数组记录 [i]\[j] 长度

注意和递归需要定义 base case一样，这里也要定义一个**基本情况**

![image-20220518150039873](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518150039873.png)

因此根据依赖关系图，可以从(0,0)开始，一行一行的算，保证后面的结果一一定来自于前面的计算

也可以从(m,n)往回递归，但要注意将已经算过了的做备忘并记录

复杂度即子问题规模为 O(mn)

![image-20220518150331746](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518150331746.png)

通过箭头事实上是用来记录最后怎么找到相应的最优情况

![image-20220518185746933](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518185746933.png)

当遇到向左上方的箭头时，就把值打印出来

## Edit distance

计算两个字符串之间的编辑距离

![image-20220518185919752](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518185919752.png)

![image-20220518190735112](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518190735112.png)

类似上面的最长公共子序列，i 表示字符串 1 的前 i 个字符，j 表示字符串 2 的前 j 个字符

![image-20220518191316446](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518191316446.png)

diff(i,j) 在 x 和 y 相同时为1 ，不相同时为0

![image-20220518191443849](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518191443849.png)

类似上面的最长公共字符串，后面的问题依赖于前面的 3 个问题，因此可以一行行着来，也可以一列列计算

### underlying DAG

![image-20220518191809472](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518191809472.png)

可以将字符相同的斜线的权值设置为 0，横和竖是对应了删除和插入，其他斜线代表了替换，都设置为 1，那么**问题就转换成了求 (0,0)到 (m,n) 的最短路径**

### :star:Finding Subproblem

![image-20220518192143413](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518192143413.png)

## Knapsack 背包问题

![image-20220518192433910](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518192433910.png)

![image-20220518193347236](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518193347236.png)

**相同物品无限个**：不用关心特定的物品。一维 DP 问题，K(w) 表示当背包容量为 w 时，所能装的最大价值，因此 **K(w) = max{K(w~i~) + v~i~}**

> ##### 注意：O(nW) 不是多项式算法，而是一个伪多项式算法

![image-20220518195134123](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518195134123.png)

**任意物品仅一个**：**那么需要关注特定的物品**，类似前面的题目，要关注这个第 j 个物品要不要放入背包中

![image-20220518195455818](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220518195455818.png)

**自底向上的算法**

- **优点：**不存在递归，看起来像递归的，都是直接使用之前计算好的。
- **缺点：**需要将所有的子问题都计算出来

**自顶向下的算法**【*上面就是一个自顶向下的背包解法，使用 hash table 存储值*】

- **优点：**如果对于有的子问题，求解过程中没有用到，那么就可以不计算
- **缺点：**需要递归调用，栈空间消耗大

