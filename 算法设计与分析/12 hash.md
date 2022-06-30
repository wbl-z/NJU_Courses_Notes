# 09 hash

![image-20220327151834052](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327151834052.png)

![image-20220327152016823](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327152016823.png)

hash结合了两者的优势，充分利用空间且常数级别的查找速度

![image-20220327152243050](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327152243050.png)

平均情况是O(1+α)【α是装载因子】，最坏情况下仍是O(n)

而O(1)在一般意义下是不可能实现的

![image-20220327152628827](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327152628827.png)

![image-20220327152959255](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327152959255.png)

hash将较大的key space映射到较小的空间中

冲突会发生

![image-20220327153349647](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327153349647.png)

![image-20220327153410934](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327153410934.png)

## closed address

闭地址/开散列：即key**所在的槽是不变的**，而是在这个槽中维护一个**链表**

![image-20220327153857257](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327153857257.png)

新插入元素是插入到链表的**头部**的，原因是**避免了要将整个链表遍历**

### 分析

![image-20220327154036072](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327154036072.png)

这里的删除O(1)是指已经**提前查找过**，并且得到了**指向这个元素的指针**，且链表为**双向链表**，因此O(1)即可删除这个元素

![image-20220327154325425](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327154325425.png)

简单一致哈希假设：即key映射到任何一个槽的概率是相同的

![image-20220327154456967](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327154456967.png)

最坏情况是Θ(n)，即所有元素在一个槽中

![image-20220327154907189](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327154907189.png)

查找失败的平均代价是Θ(1+n/m)=Θ(1+α)

![image-20220327155259592](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327155259592.png)

一个元素平均查找成功的代价是1(计算hash)+在它插入后，再插入到表中的元素个数\*插入代价(1)\*插入到这个元素相同链表的可能性(1/m**[简单一致哈希假设]**)，*即链表中，在这个元素前面的元素的个数*

![image-20220327160251880](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327160251880.png)

## open address

开地址/闭散列：即不使用链表，将key计算得到的槽的地址“打开”，可以放到其他的地方去

![image-20220327160423063](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327160423063.png)

![image-20220327160814726](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327160814726.png)

装载因子**小于等于1**

![image-20220327160912827](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327160912827.png)

**i是从0~m-1的**，即最多进行**m次**探测

![image-20220327161234878](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327161234878.png)

对于线性探测和二次探测，只要初始的位置确定了，那么整个探测序列是确定了的，共有m个槽，因此有**m种探测序列**（每个初始位置一个探测序列）

而对于双重散列，初始位置确定后，其探测间隔仍然是取决于key的，因此探测间隔有m种可能（h~2~(x)仍然是0~m-1的），同时初始位置有m种可能，因此共存在着**m^2^种探测序列**

![image-20220327162121041](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327162121041.png)

**一致哈希假设**：理论上，探测序列有m!种，因为比如第一次探测有m个位置可以选，剩下m-1个位置可以选……，一致哈希假设即对于任意的key，它的探测序列是m!中的一种的可能性是一样的

**一致哈希假设是简单一致哈希假设的一般化**

前面的探测方式，**不满足一致hash假设**，因为可以看到它们的可能性只有m/m^2^，自然不可能涉及m!，事实上m!种也是无法达到的

### 分析

![image-20220327162205329](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327162205329.png)

对于离散型变量的期望的转换

![image-20220327163011115](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327163011115.png)

不成功的概率，**当查找到位置为空的时候就停止查找了**，因此查找不成功的可能探测次数为1~m，α的等比数列求和，**即$\frac{1}{1-\alpha}$**

![image-20220327165526401](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327165526401.png)

**这个过程和查找一个元素的过程完全一致**，插入一个元素是一直查找，直到找到一个空位把这个元素放进去为止

![image-20220327165538815](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327165538815.png)

同样考虑插入的顺序，因为**后面插入的元素不影响前面的元素的查找**，在要查找第i+1个元素时，前面已经插入的i个元素会影响到i+1个元素的查找，因此**找到这个第i+1个元素所需要的cost和插入它的代价一样，也和在有i个元素的hash表中查找这第i+1个元素的代价一样(此时表中有i个元素，$α=\frac{i}{m}$)**

故**查找成功的代价为$\frac{1}{\alpha}ln\frac{1}{1-\alpha}$**.*（可见在只有一半的元素时，查找的次数为1.3，即使是90%满的时候，查找的次数也为2.5）*

![image-20220327170344542](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327170344542.png)

对于开地址，删除元素时会有问题，即不能直接删去，需要加上一个标记，防止后面插入并且到达过这个位置的元素不能被找到。但如果加上了标记，那么**查找的复杂度就不取决于装载因子了**，而取决于原来插入过的元素

**因此在有删除元素需去时，尽可能使用闭地址**

## Amortized Analysis 均摊分析

![image-20220327171743118](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327171743118.png)

![image-20220327171528441](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327171528441.png)

蛮力计算出插入元素的总和为3n，那么平均每个元素插入的代价为3

### the accounting method 记账法

![image-20220327172435737](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327172435737.png)

事实上是一种放缩思想，给每个操作增加了一个想像出来的**新代价**，要求：

1. 新代价ac~i~可能是负值，但$\Sigma$ac~i~必须是非负的，即不能让总代价变小
2. 新代价+原代价的求和要容易计算

例如:

![image-20220327172713143](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220327172713143.png)

条件一可以用数学归纳法证明：不妨假设n个元素时成立，那么从n->2n，再插入n个元素时，会使得cost增大2n，而在2n->4n时是-2n+2，因此刚好和前面的2n抵消，因此可以保证总和大于等于0；

条件二显然

因此可以用均摊分析得到每一次插入的平均操作次数