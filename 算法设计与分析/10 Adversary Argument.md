# Adversary Argument

## P1

![image-20220324170001833](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324170001833.png)

![image-20220324170224279](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324170224279.png)

决策树只能给出需要至少一次peek，即如果中间的bit是0，那么这次bit串一定不包含111

因此需要对手论证来得到对于所有情况，至少需要几次peek，能保证得到b是否包含111

![image-20220324171536412](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324171536412.png)

对手策略：![image-20220316143242057](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220316143242057.png)

因此如果只看3次的话，x中会有连续3个1 ，y中没有连续3个1，那么只看3次，符合这3次peek结果的bit串，就存在着两种情况下x，y，一种包含111，一种不包含111，因此无法判断

### 证明

![image-20220324171904717](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324171904717.png)

如果翻转flip3次，y中有3个1，那么每次翻转都是要翻转y中的，根据对手论证，那么必须要存在3个位置，其中的任何一个在x中翻转后都会导致x中不包含11111，而事实上肯定不存在。*即使第一次peek第3位，那么第二次peek任何其他位置都不会导致x没有3个连续1*

因此y中不可能包含3个1，更不可能有3个连续的1

![image-20220324172544533](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324172544533.png)

**决策树：**

- 注意这里的决策树是用来说明对于**这个Solution算法**的最坏情况复杂度的；
- 对于单个决策树，下界是它的**最坏情况深度**（*如最开始只要一次就可以判断即看中间bit=0，就判断不包含是最好的情况，而不是最坏的情况*）

**对手论证：**

- 而对手论证是用来说明**对于所有解决这个问题**的最坏情况复杂度的；
- 对手论证是说 对于所有的决策树深度的**最小值**（*有的算法非常糟糕，当然复杂度会比这个问题的下界更复杂*）是下界

## P2

![image-20220324174104217](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324174104217.png)

问题：对于无向图的邻接矩阵，一次看n\*n矩阵*（因为是无向无自环图-因此只有$\frac{n(n-1)}{2}$条边要看）*中的一个数字，至少要看多少次才能判断图是否连通？

![image-20220324175301668](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324175301668.png)

Y是空图，M是完全图

![image-20220324175518369](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324175518369.png)

首先来证明5条不变式invariants，它们在算法的任何时候均成立

- 第3条，如果M中有环，那么Y中不可能有环上的边，因为如果有的话，那么是怎么来的呢？只能是在M中不能删去时才会加在Y中，而环上的边是可以删去的（仍然保证连通性），因此是不可能的。**同时**也意味着算法到现在没有查看过环上的边，因为如果查看了，肯定会删去导致这个环不存在
- 第4条显然，因为Y是M子图，如果Y有环，那么M肯定有这个环，而根据第3条，这是不可能的
- 第5条，只有算法把所有的边都查看一遍，Y才会等于M，因为如果有边e没查看，那么一定是在M中有这条边e，而Y中没有e，不可能Y=M。**然后**使用反证法：如果Y连通无环，那么Y就是树，Y不等于M，那么一定M比Y多边且Y是M的子图，那么M必然是有环的，因为在树上多加任何边都会形成环，然而这个环的其他边却在Y中，与3矛盾

因此在没有把所有的边看完时，对于Y和M，都符合观测结果，因此无法判断。**所有一定要把所有的边都看完才能判断图是否连通**

> 同样注意：比如要判断的图是个空图，那么只要观测到剩下n-2边没观测就能判断这个图不连通，因为n个顶点的连通图至少n-1条边。**但这是最好情况**，**对手论证说明的是所有解决这个问题的算法的最坏情况**

![image-20220324181702391](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324181702391.png)

Aanderaa-Karp-Rosenberg猜想：every nontrivial monotone property of v-vertex graph is evasive*所有的非平凡单调的图的性质都是evasive的，即要查看所有边才能确定*

## P3

![image-20220324195707933](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324195707933.png)

3)每次询问都一定能排除一个人，如果A认识B，那么A肯定不是名人，如果A不认识B，那么B肯定不是名人。

- 所以**最少只要n-1**次询问就可以找到名人，即我们恰好选中名人去与他人判断。
- 如果不是这样，那么n-1找到最后一个人后，还需要讲这个人和其他所有人都问一次，确定这个人是不是名人（可能一个名人都没有），**即n+n-1=O(n)**

## P4

![image-20220324201631216](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324201631216.png)

![image-20220316151218445](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220316151218445.png)

至少要**比7次**

5匹马5组比一次，5组中最快的5匹马比一次，即可得到最快的一匹马，然后将剩下的绿色和蓝色的马一起比一次，即可得到最快的2匹马为第二第三快。

因为D1，E1已经输给了3匹马，不可能是第二、三，而B1有可能第二，那么B2有可能是第三，A1第一，那么B2，B3有可能第二、三，因此这5匹有可能是第二、三的马比较即可

## P5

![image-20220324202306428](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324202306428.png)

![image-20220324202740696](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324202740696.png)

1)一次可以排除掉4个元素，因此一共需要排除掉n-1个元素，共需要(n-1)/4次

2)**共有log5n个元素是与最大数比较过并排第二的元素**（类似找第二大元素，至少有logn个元素直接输给过max），（log5n-1）/4次即可找出其中的最大值，即整体第二大

## P6（自己思考todo）

![image-20220324202845274](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324202845274.png)

构建对手论证

![image-20220325114202424](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325114202424.png)

![image-20220324203200710](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324203200710.png)

个人想法：如果少于一半，那么可以两两分成一组，一定会有好-好的组合，可能会有坏-坏的组合，即将第一种情况的组合取出来，再两两匹配取出来，直到所有的组合都是第一种情况，然后进行全部组合分组C(n,m)，确保其中没有坏-坏的组，即得到了好的芯片，用这个好的芯片去检测所有芯片

## P7带权中位数

![image-20220324203546995](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324203546995.png)

带权(下)中位数

![image-20220324203704785](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324203704785.png)

![image-20220324204327229](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324204327229.png)

![image-20220324204903362](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324204903362.png)

:star:**每次使用最坏情况线性时间去找到常规的中位数Θ(n)（当然找第K大的元素都是Θ(n)），然后根据这个中位数划分成两半**，判断带权中位数在哪一半，==从而将问题规模减小一半==，但注意要把大于X~k~的权重都加到X~k~上，保证权重不变

## P8

![image-20220324205157984](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324205157984.png)

1)

- 可以直接遍历
- 也可以采用二分查找，**看n/2个元素，如果比n/2大**，说明最小未出现的自然数在前一半，**如果等于n/2**，那么说明在后一半

2)

- 直接打表，构建一个0~n-1的数组，出现一个数就标记一个数，全部打完表，即可遍历一遍数组找到最小的**（其实就是计数排序）**
- **采用O(n)找中位数**，然后采用(1)中的法2即可

## P9 找出前K大的排好序的数

![image-20220324205725594](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220324205725594.png)

- 排序
- 构建最大堆O(n)，取堆顶后拿最后一个元素下滤(logn)，即相当于只对前K个元素进行堆排序
- 使用O(n)找到第K大元素，然后partitionO(n)，得到前K大的元素，再对这K个元素排序O(klogk)

