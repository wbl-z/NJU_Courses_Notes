# 13 union-find

![image-20220328102036890](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328102036890.png)

如何搜索一个动态等价关系？

![image-20220328102433333](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328102433333.png)

在一面墙都没推到之前，有25个等价类，每推倒一面墙，就会将两个等价类合并

![image-20220328103021679](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328103021679.png)

使用等价类判断两个点是不是等价类，如果是等价，那么说明这两个点已经连通

![image-20220328103312102](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328103312102.png)

![image-20220328103327053](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328103327053.png)

- is:判断两个元素是不是等价的，属于一个等价类
- make:将两个等价类合并

![image-20220328103730499](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328103730499.png)

- matrix实现：即将相同等价类的位置上存储的值改为相同，如合并3、5，那么就把3-5和5-3都改成1，同时还要找到所有和3、5已经属于同一个等价类的元素，把它们都改成1，因此每次make操作最坏可能是O(n)，那么m次就是O(mn)；当然is指令速度很快，只要看3-5和5-3是不是1，O(1)即可
- array实现：使用数组存储每个元素所属等价类的id，因此make时需要扫描整个数组，类似matrix方法O(n)，is操作只要看两个元素的id是否相同即可O(1)
- union-find

![image-20220328104718995](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328104718995.png)

create相当于n次makeSet，两者相当于是构造函数

**find会得到元素e所在的等价类的根节点root**

**union是将两个等价类的根节点root合并，一般是前者变成后者的child**

如下is和make可以由find和union实现

![image-20220328104944457](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328104944457.png)

![image-20220328105213435](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328105213435.png)

**研究对象是有m个操作**（可以是find和union中任意数目）的input

**评价指标：m个操作中访问父节点的次数/代价**

![image-20220328105836176](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328105836176.png)

n是makeSet，n-1是union n-1次，(m-n+1)n是n次find，即Θ(mn)

可见简单的union和find操作效率不高，和matrix和array实现的最坏情况复杂度一样

**改进要点：让树的高度不那么高**

### weight union

![image-20220328110231387](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328110231387.png)

**让节点少的等价类的根节点指向节点多的等价类的根节点**，因此这里union需要进行修改

n是makeSet，union(1,2)需要查看1和2的父节点，然后合并，故为3，union(2,3)同理也是3，而后面的如union(3,4)，那么要看3和4的parent，3需要看两次，4一次，合并一次，故后面为4(n-3)

![image-20220328111541557](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328111541557.png)

**使用weight union的方式得到的树（不一定是二叉树，如果是多叉树，那么高度更低）的高度不会超过logn**

![image-20220328112251684](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328112251684.png)

因此对于m次的操作，复杂度为Θ(mlogn)【其中union操作的复杂度为1，这里要求union的节点是根节点并且包含权重表示有多少个节点】。再加上makeSet Θ(n)，故为**Θ(n+mlogn)**

### path compression

**改进find**

![](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328113952671.png)

cFind的cost为原来的find的2n-1，要把沿路上的元素都挂到根节点上，**但事实上cFind的执行次数是很少的**，如执行一次后，后续对于v，w，x的查找都不需要用cFind

![image-20220328114145093](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328114145093.png)

对于上面这样高cost的操作执行少，低cost的操作执行多的情况，适合使用均摊分析

![image-20220328114448721](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328114448721.png)

**log*(n)是非常小的，几乎可以看成常数**，因为H(i)的增长非常快，而log\*(n)是满足H(k)≥n的最小的k

如下可见，在65537到2^65536^之间的n，log*(n)都为5

![image-20220328114815284](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328114815284.png)



![image-20220328115037461](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328115037461.png)

均摊分析过程很复杂，这里给出均摊分析中的记账代价和均摊代价，可见所有3个操作的均摊代价都不超过1+4log*(n+1)，因此总共的上界为(n+m)(1+4log\*(n+1))

*【因为makeSet是对每个元素的操作，所以共要n次，其余两个操作共m次，故m+n】*

![image-20220328115550248](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220328115550248.png)

结论：**对于wUnion和cFind的并查集中m次操作和n个元素，那么复杂度为O((n+m)log*(n))**

