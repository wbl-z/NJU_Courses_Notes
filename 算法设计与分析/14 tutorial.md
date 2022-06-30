# 14 tutorial

## hash

### P1

![image-20220330194726421](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330194726421.png)

要求装载因子为0.7，总共7个key，因此hash表的长度为10

![image-20220330194734822](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330194734822.png)

**查找成功即把7个数都查找一次**，代价求和，查找每个数的概率是1/7

**查看不成功即要查找不在hash表中的元素**，因为hash表的**长度为10，可以分成10种情况**（求和除以10即可得一次查找不成功需要的代价），根据线性探测，找到第一个空的槽停止（即说明这个数不在hash表中）
*如hash计算出为0，看0号槽，有元素，则看下一个槽，一直看到6停止，故代价为7*

**总的**查找代价即为**查找成功的代价\*查找成功率+查找不成功的代价*（1-查找成功率）**

### P2

![image-20220330200157374](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330200157374.png)

![image-20220330200207352](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330200207352.png)

![image-20220330200214773](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330200214773.png)

2.6hc/3才是开地址哈希槽的数目，2.6hc是所占的空间大小

## universal hashing 全域散列

![image-20220330200555172](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330200555172.png)

既随机又一致 random & consistent

![image-20220330200827548](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330200827548.png)

没有哪个hash函数能够在任何情况下都表现得很好

![image-20220330203011037](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330203011037.png)

![image-20220330202953800](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330202953800.png)

x个元素，那么选定比x大的素数n，在0~n-1之前随机选定系数构成散列函数，那么会导致冲突的情况的概率为1/n

#### 来自[Universal Hashing全域哈希原理与python实现](https://blog.csdn.net/MustImproved/article/details/105226276)

![image-20220331144932181](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220331144932181.png)![image-20220331144954034](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220331144954034.png)

![image-20220331145113499](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220331145113499.png)

## amortized analysis

![image-20220330203354563](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330203354563.png)

使用均摊分析适合的场景

### accounting method记账法（考试会考）

**原理**：**cost小的操作次数多，cost多的操作次数少，将cost大的平摊到cost小的操作上**

![image-20220330203540614](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330203540614.png)

#### 例子：Multipop Stack

![image-20220330203712763](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330203712763.png)

多了一个multipop操作，同时弹出s个元素，如果栈所有的元素数目少于s，那么弹出所有元素

![image-20220330203758631](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330203758631.png)

![image-20220330204059909](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330204059909.png)

accounting cost的和是非负的，因为pop和multipop一定要有push，因此pop刚好和push抵消

因此可以得到每次操作的**平均代价不超过2**

#### Graph operation

![image-20220330204750213](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330204750213.png)

将cost很大的disconnect操作均摊到connect上，任何一条边要删除先要加进来

![image-20220330204906467](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330204906467.png)

因此均摊分析得到的单个操作的**平均代价就是3**

#### Implement a Queue with two Stacks

![image-20220330205214928](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330205214928.png)

![image-20220330205824520](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330205824520.png)

![image-20220330210746892](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330210746892.png)

下面的平摊法代价更低，即**平摊最好是让每个操作的代价相近，从而使得平均代价最小，得到最小的上界，而不是让一个操作得到所有代价，其他操作的代价为0**

因此下面的分析方法一次操作的最多代价为3，而不是上面分析的4（n次操作，代价最多为3n）

### Aggregate Method 聚集法

![image-20220330211300225](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330211300225.png)

对于上面的Multipop Stack，一个元素最多被pop一次（无论是pop还是multipop），且pop的次数最多为push的次数，而总共n次操作，因此最多n次push和n次pop（**考虑超出情况，便于分析得到上界**）也就2n的cost，2n/n=2，因此一次操作最多cost=2

#### Binary Counter

![image-20220330211623754](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330211623754.png)

使用均摊分析也可以处理，**从1变成0一定有从0变成1** ，因此均摊代价为2

> 不能用1/2和-1/2，因为这样的话1到0的均摊代价不是1，而在二进制计数器中不是以0到1和1到0作为基本操作的，所以n个操作，到底有多少个1到0是不知道的，那么就求不出来总的均摊代价

![image-20220330212351111](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330212351111.png)

#### Potential Method 势能法（不做要求）

![image-20220330213002498](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330213002498.png)

![image-20220330213009633](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330213009633.png)

对于array doubling问题：

![image-20220330213752559](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330213752559.png)

对于势能函数**Φ(D~i~)一定≥0**，**因为2的logi取上整次方不到达2i，最大的情况也仅仅为2(i-1)**

## union find

![image-20220330214945981](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330214945981.png)

![image-20220330214952121](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330214952121.png)

均采用并查集即可

![image-20220330215010773](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330215010773.png)

![image-20220330215022888](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220330215022888.png)

