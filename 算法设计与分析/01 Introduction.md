# 01 Introduction

## introduction 

![image-20220214172418965](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214172418965.png)

如果有一个算法，那么需要问三个问题，如果三个问题都能满足我们的要求，那么这个算法就过关了：

- 是否正确
- 时间复杂度如何
- 能不能做得更好

![image-20220214172306867](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214172306867.png)

![image-20220214172828468](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214172828468.png)

递归为指数时间代价，因为过程中出现了很多的重复计算，都是无用功；改为迭代后可以降低为线性时间代价

![image-20220214173332303](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214173332303.png)

## goal of the course

![image-20220214173517465](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214173517465.png)

1. 解决频繁出现在CS中的实际问题
2. 通过学习基本的原则和技巧来回答这个算法到底有多好/多坏
3. 了解NPC问题

![image-20220214173608644](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214173608644.png)



![image-20220214173643973](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214173643973.png)

设计和分析是交替的，紧密联系的



![image-20220214173838862](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214173838862.png)



![image-20220214174004985](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214174004985.png)

- 正确性
- 时间复杂度
- 空间复杂度
- 简洁性，清晰性
- 最优性

**最关注1，2，5**

### correctness

![image-20220214174542115](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214174542115.png)

使用数学归纳法证明算法的正确性（通常）

### amount of work done

![image-20220214174652735](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214174652735.png)

![image-20220214174756366](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214174756366.png)

以关键操作作为计算时间复杂度的操作，如矩阵乘法中的乘法就是关键操作（相比于加法耗时长，且如果知道了乘法的个数，那么加法往往是乘法的常数倍）

![image-20220214175159486](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214175159486.png)

运行时间往往与关键操作的个数成比例（proportional）

![image-20220214175249459](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220214175249459.png)

- 时间复杂度往往依赖于输入的大小
- 时间复杂度不仅仅依赖于输入的大小

最坏时间复杂度

平均时间复杂度

![image-20220215162956334](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220215162956334.png)

ex：

![image-20220215163103347](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220215163103347.png)![image-20220215163326001](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220215163326001.png)![image-20220215164758952](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220215164758952.png)

### optimality

![image-20220215164912799](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220215164912799.png)

- 对于问题P，用于解决P的算法A在最坏情况下的运行时间为W
- 对于解决问题P的任何一个算法，对于P的大小为n的输入的最小运行时间为F
- 如果W=F，那么A是最优的算法，同时根据第二条可知F是问题P的lower bound

W刻画了算法A在最坏情况下的运行时间，而F刻画了问题P的本质，不管什么算法，总存在一个输入，使得这个算法需要F(n)的运行时间

![image-20220215165751738](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220215165751738.png)

如果不相等，那么说明A不是最优的，也可能是F(n)的lower bound找的不对

![image-20220215170245727](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220215170245727.png)

下面是找到问题的下界，至少需要n-1次的比较，否则可能会有错误的结果，因此下界为n-1。

而上面的算法的比较次数始终为n-1，即最坏情况也是n-1，因此W=F，这个算法就是最优的算法

![image-20220215170516744](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220215170516744.png)

