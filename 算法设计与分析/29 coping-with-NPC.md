## 29 coping-with-NPC【不考】

**对于优化问题，可以有所妥协**，可能不能在多项式时间内解决，比如求权值最小的某个回路是15；但经过一些妥协，如求权值不超过最小的两倍即30是可以在多项式时间内解决的。

![image-20220609212548971](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609212548971.png)

三种方法处理 NPC：

1. 穷举法
2. 近似
3. 启发式，根据经验设计启发算法，不能保证结果和最优值接近，性能也可能是任意差的

### Intelligent exhaustive search 智能化地穷举搜索

![image-20220609212940423](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609212940423.png)

**4 个变量，因此只要验证 2^4^ 即可，并且并不是验证所有的 2^4^**，根据其中的情况智能地抛弃一部分可能，比如 w=1，z 不论取什么就不可能成立，因此不用看 x 和 y 了

### Approximation 近似算法

![image-20220609213343469](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609213343469.png)

近似率，对于任意的输入，都不会超过近似率，即近似率是所有输入比值的最大值

#### example 1

![image-20220609213459790](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609213459790.png)

![image-20220609213553176](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609213553176.png)

一组不相交【即没有公共顶点】的边就是图的一个**匹配**

每次加入一条边 u,v 后把所有的与 u 和 v 相连的边都删去，这样就能保证是匹配

![image-20220609214027299](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609214027299.png)

![image-20220609215025151](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609215025151.png)

近似率为 2，即这个算法得到的顶点覆盖的大小最多是最优解的两倍。因为 A 是一个匹配【当然不一定是最大匹配】，顶点 C 的大小是 A 的两倍，因为每次选出两个顶点，而匹配都为 |A| 了，那么至少肯定要这么多个顶点才能点覆盖（一个顶点最多覆盖一条边），而这又不一定是最大匹配，因此上图的比值小于等于 2

#### example 2

![image-20220609215512021](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609215512021.png)

![image-20220609215824914](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609215824914.png)

最小割问题：是 P 问题

找到一个顶点划分使得两部分之间的割数量最小

##### 随机算法：

![image-20220609215928182](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609215928182.png)![image-20220609220049841](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609220049841.png)

这个随机算法中的一个操作：contract(e) 是将 e 两边的顶点合并在一起

![image-20220609220056304](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609220056304.png)

![image-20220609220307233](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609220307233.png)

虽然一次算法操作返回 min-cut 的概率是 $\frac{2}{n(n-1)}$ ，但可以重复执行 $\frac{n(n-1)}{2}$ 次，**都不能得到 min-cut 的概率是 $\frac{1}{e}$** 说明这个算法的成功率还是很高的

##### 下面证明算法返回 min-cut 的概率

![image-20220609220609844](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609220609844.png)

**引理 1**：如果有 min-cut 为 k，那么任意一个顶点的度都至少为 k，否则如果有顶点度数为 k-1，那么直接把这个顶点割出来，就形成了大小为 k-1 的 min-cut

**引理 2**：收缩操作不会使得最小割的大小变小【*收缩操作就是把一些点划分到一起，经过v-2 次收缩就是将图分成两部分了*】

![image-20220609221930218](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609221930218.png)

![image-20220609221937203](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609221937203.png)

每一轮都没有把 min-cut 收缩掉的概率全部乘起来

### 两种随机算法

![image-20220609222140463](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220609222140463.png)

![image-20220610102555815](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610102555815.png)

要对比两个数据库中的数据是否是一样的

![image-20220610102944484](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610102944484.png)

![image-20220610103243591](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610103243591.png)

![image-20220610103325992](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610103325992.png)

当 |x-y| 是 p 的倍数时，那么 x 和 y 即使不一样取模后结果一样

如果 k > n，那么可以放缩成 p~1~ · ... · p~n~，所以至少有 n 个质数，如果从小到大排列乘，那么第一个质数肯定大于等于 1，第二个质数肯定大于等于 2，依次下去，得到 n! 

![image-20220610103920611](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610103920611.png)

Prim(n^2^) 是计算 1-n^2^ 之间的质数数目的公式

### Heuristics 启发式

![image-20220610104247212](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610104247212.png)

![image-20220610104736751](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610104736751.png)

如果两个解之间只变换一个节点就能到达，那么它们就是解空间中的邻居

![image-20220610104750998](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610104750998.png)

![image-20220610104756542](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610104756542.png)

上面是某一次找的过程中在此时，不论它在解空间中的哪个邻居，都不会比当前解的 cost 小，因此当前局部最优就是 2

![image-20220610104909765](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610104909765.png)

如上启发式算法可能会到达局部最优，在有的情况下可能可以到达全局最优

#### 处理局部最优解

1.  **可以随机化，并重复多次**

![image-20220610105054318](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610105054318.png)

2. **模拟退火**

![image-20220610105135538](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610105135538.png)

如果 s' 比 s 差，那么在启发式算法中一定不替换，这样可能会陷入局部最优

模拟退火在 s‘ 比 s 差时以一定的概率进行替换，并且和两者的差值 Δ 有关，Δ越大，就越不可能用 s’ 去替换 s。此外参数 T 表示温度，随着时间推移温度下降【替换的概率下降】，即在程序最开始允许大概率的替换，来避免局部最优，后面概率下降。

![image-20220610105617338](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220610105617338.png)