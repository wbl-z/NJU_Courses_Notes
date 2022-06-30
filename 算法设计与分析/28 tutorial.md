## 28 tutorial

![image-20220601115200401](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220601115200401.png)

### what makes a problem hard

#### example 1

![image-20220601115446501](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220601115446501.png)

SAT 的特例：

3 SAT 是指每一个 clause 里面最多 2 个变量

- 3 SAT 是 NPC 问题
- 2 SAT 是 P 问题

#### example 2

![image-20220601120127803](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220601120127803.png)

旅行商问题：给定一个**完全图**，找到哈密尔顿回路并且代价不超过 b

哈密尔顿回路可以看作是一棵特殊的树(每个节点的**度数一定是 2**)，TSP 问题就像是找到一棵形状受到限制的 MST

这个限制使得 P 问题变成了 NPC 问题

而且 TSP 问题事实上是 NPC 中较难的一类问题

#### example 3

![image-20220606163029747](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606163029747.png)

在所有边的长度都是非负的图 G 中，且要求下面的路径都是 **simple** 的，即简单的，**路径上没有重复节点的**

最短路径问题：s 和 t 之间是否存在长度小于 g 的路径：P 问题，用 dijkstra 算法求最短路径即可

**最长路径问题**：s 和 t 之间是否存在长度大于 g 的路径：**NPC 问题**

#### example 4

![image-20220606163447449](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606163447449.png)

给定二分图 G 共 2 n 个顶点

二维匹配和三维匹配

#### example 5

![image-20220606163805320](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606163805320.png)

哈密尔顿回路问题：NPC

欧拉回路：P【遍历所有边，每个边只被遍历一次，顶点可以被多次遍历】

### Reductions

![image-20220606174724253](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606174724253.png)

虽然规约的定义中的问题是指决策问题，事实上对于优化问题使用规约到 Q 来解决也是可以的

#### example 1

![image-20220606174842481](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606174842481.png)

哈密尔顿路径问题：给定一个无向图 G，对于顶点 s 和 t，是否存在 s 到 t 的路径，这个路径经过 G 中的所有点有且仅有一次

规约方式：**增加一个顶点与 s 和 t 相连**

![image-20220606175530360](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606175530360.png)

**直接连接 s 和 t 是不可以的**：从左边推到右边没问题，但是从右边不能推到左边：因为比如上面的 G 中可以显然看到最外面一圈路径构成了哈密尔顿回路，并且显然没有用到 st 这条边，因此去掉这条边，不代表就构成了哈密尔顿路径，比如图 G 中最中间的点就不能被 s 到 t 的哈密尔顿路径经过

#### example 2

![image-20220606175836392](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606175836392.png)

**最大独立集问题**:图 G 有没有大小为 g 的独立集
独立集：集合中任意两个顶点**之间**都没有边

**最小点覆盖问题**：能否找到 k 个顶点，这个 k 个顶点可以覆盖图 G 中所有的边，如上图例子左边的两个橙色的点就覆盖了所有的边

 **G - (最大)独立集 = (最小)点覆盖**

因为独立集中间的任意点都没有边，所以边一定在外面，外面的所有点就能覆盖所有的边

因此可以实现规约

#### example 3

![image-20220606212759621](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606212759621.png)

独立集规约到最大团问题，只要将原图 G 取反 G‘ 求最大团即可得到原图 G 的独立集

#### example 4

![image-20220606213327147](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606213327147.png)

联系 3-SAT 问题到最大团问题的方法，但是这时候因为是独立集，因此图的构建方法和规约到最大团时**相反即可**。

对于 3-SAT 中的每个子句，建立子句中变量数目的顶点，它们一起作为图的一个顶点：且一个子句的顶点内一定有边相连；在不同子句中的两个顶点之间的值刚好是是 x~i~ 和 x~i~ 取反时【即不能同时取真】有边

![image-20220606214404739](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606214404739.png)

对于独立集问题中的 g，就可以设置为 3-SAT问题中的子句数目 g。

【和规约到最大团一样，有 k 个子句的 3-SAT 问题可以规约到图 G 有大小为 k 的最大团】

后续的证明：

- 3-SAT 到独立集：如果 g 个子句的 3-SAT 能满足，说明每个子句中一定至少有一个成真的，那么这些成真的顶点之间肯定不会有边，**所以这 g 个顶点就构成了大小为 k 的独立集**【注意：**规约到的独立集问题是决策问题**，即是否存在大小为 g 的独立集即可，而不是最大独立集的优化问题】
- 独立集到 3-SAT：如果图 G 存在大小为 g 的独立集，因为一个子句的三个顶点之间一定是相连的，所以这 g 个顶点一定分布在 g 个子句中才行

#### example 5

**比较特殊的规约，是相同问题不同限定下的规约**：一般意义的 SAT 问题规约到 3-SAT 问题。

说明如果能解决 3-SAT 问题，所有的 SAT 问题都能解决了

![image-20220606215323645](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606215323645.png)

![image-20220606224106903](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606224106903.png)

对于 SAT 问题中如果所有的子句的变量小于等于3，那么可以直接输入到 3-SAT 处理。

对于存在子句的变量大于 3 的 SAT 问题，可以通过上面的方式转换：不妨设这个 SAT 问题为 k-SAT 问题：

转换方式：**增加新的 k - 3 个变量 y~1~...y~k-3~**。变成上面的形式，形成新的 k-2 个子句

证明：

- 左边有成真指派→右边有成真指派：左边为真，那么至少有一个变量为真，不妨设为 a~i~，那么对于右边的新增变量 y ，令 y~1~ 到 y~i-2~ 都为 true，其他为 false。

  那么对于右边的式子的第一个到第 i-2 个子句都为真，因为一个子句中第三个变量 y 是真。

  第 i-1 个子句的第一个元素会是 y~i-2~取反，为假，第二个元素是 a~i~ 为真，第三个元素是 y~i-1~ 为假。

  第 i 个子句到后面的所有子句，因为 y~i-1~ 到后面都为假，因此后面所有子句的第一个元素都为真（因为是取反）

  所以右边也存在成真指派

- 左边有成真指派←右边有成真指派：反证法，如果右边存在成真指派，但左边不存在， 那么所有的 a 都是假，反观右边式子，那么第一个子句 y~1~ 必须为真，从而 y~1~ 取反为假，y~2~ 必须为真……，到最后一个子句 y~k-3~ 为假，但最后一个子句中所有都为假了，因此最后一个子句一定为假，右边不存在成真指派。矛盾

#### example 6

![image-20220606230128240](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606230128240.png)

决策问题：是否存在一个子集的**和刚好是 C**

![image-20220606230615816](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606230615816.png)

决策问题：是否存在一种任务调度方式，使得惩罚**小于等于 k**

**注意上面两个问题的决策问题的区别**

转换方式：

![image-20220606231012311](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606231012311.png)



证明：

- 子集和问题→任务调度问题

  ![image-20220606231017963](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606231017963.png)

  对 J 内的 job 先执行，顺序任意，然后执行 J 外的 job。

  对于 J 内的 job 全部的时间和是 C，因此不会超时，对于 J 外的 job 此时都会超时，因为 ddl 都是 C，它们的惩罚加起来就 S-C，而 k 就是 S-C，因此不会超过 k

- 子集和问题←任务调度问题

  ![image-20220606231647913](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220606231647913.png)

  不妨设前面 m 个 job 不超时，后面的 n-m个 job 超时，因此前面的 m 个 job 的时间和小于等于 C，后面的 job 的惩罚和【当然也是时间和，因为转换是如此】小于等于 k = S-C【因为任务调度问题此时是 yes】。

  将两个不等式加起来，就有全部 s~i~ 的和小于等于 S，而事实上就等于 S，因此这就要求两个不等式都必须等于，如果一个严格小于，那么另一个一定是大于。

  所以就存在子集的和为 C，子集和问题成立