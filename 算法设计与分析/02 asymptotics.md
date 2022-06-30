# 02 asymptotics

![image-20220218114140232](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218114140232.png)

三个符号实际上表示的是集合

![image-20220218114253951](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218114253951.png)

比较两个算法的时间复杂度

根据一些原则来简化分析：

- 假定整个的运行步骤是和基本操作的数量成比例的，因此只需要关注基本操作的数量
- W/A表达式往往比较复杂，仅关注起主导作用的项
- 常系数往往被忽略

## Big Oh

![image-20220218114929207](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218114929207.png)

O描述了所有**渐进增长速度**不超过O(g)的函数

![image-20220218115150158](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218115150158.png)

![image-20220218115302663](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218115302663.png)

![image-20220218115346748](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218115346748.png)

对数的增长速度一定比幂次慢，幂次的增长速度一定比指数慢（由e^x^、x、lnx的图像理解）

渐进时间复杂度只是刻画了在**n足够大**之后，两个函数之间的关系，不表示任何时候的大小关系

![image-20220218115751823](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218115751823.png)

## Ω和Θ

![image-20220218115931015](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218115931015.png)

尽管这些符号表示的都是集合，但我们往往把写成f=，而不是f∈，这样更加直观

大O和大Ω是反过来的，小o和小ω也是反过来的

![image-20220218120152188](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218120152188.png)

而纯红色的部分就是小ω，纯蓝色的部分是小o

## properties

![image-20220218120555244](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218120555244.png)

- 传递性
- 对称性
- 有序性

![image-20220218120757634](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218120757634.png)

Θ刻画了等价类

![image-20220218164631949](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218164631949.png)

将n个数划分成j个数为一个组的区间，找到被查找元素所在的区间，再在这个区间里面顺序查找，即n/j+j是最坏情况。当j=根号n时，n/j+j是最小的

事实上，对于每一个区间，同样可以采用这样的方式，递归查找，进而产生了二分搜索

![image-20220218164947110](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218164947110.png)

先要确定first和last是合法的，增强程序的**鲁棒性**

![image-20220218165501352](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218165501352.png)

最坏情况是lgn次，每次去掉一半的元素

![image-20220218165633060](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218165633060.png)

![image-20220218172714896](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218172714896.png)

![image-20220218172802657](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218172802657.png)

那么现在要证明二分查找已经是最优的算法了：已知二分查找的最坏时间复杂度为lgn，那么只要证明对于一个有序查找，不论什么算法，一定至少需要lgn的时间即可

引入决策树来证明

![image-20220218173031429](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218173031429.png)

右边的决策树实际上就是一个二分查找的过程

算法的执行过程即从根节点到叶节点，那么从根节点到叶节点的最长路径就是最坏时间复杂度

![image-20220218173502077](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218173502077.png)

**不管什么算法，都能用决策树表示出来**

由上面的分析，p>=lg(n+1)，即有序查找至少要比较lg(n+1)次，而二分查找的最坏时间复杂度即lg(n+1)，因此二分查找是最优的

![image-20220218174323956](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220218174323956.png)

反证法：给定两个一模一样的数组，使得其中的第i个不一样，因为i没有出现在决策树中，因此两个数组的决策树是一样的，即结果一定是一样的，但两个数组并不是完全相同的，结果至少会出现一个不一样，因此矛盾，即证得对于n个的输入，决策树上至少包含n个元素

