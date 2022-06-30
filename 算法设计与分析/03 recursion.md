# 03 recursion

## outline

![image-20220222192111582](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222192111582.png)



![image-20220222192328799](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222192328799.png)

## solutions of recurrence equation

![image-20220222200332660](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222200332660.png)

关键操作为加法，而不是除法，因为除以2可以直接通过移位操作来实现，速度很快

![image-20220222200421913](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222200421913.png)

### backward substitutions后项替换法

![image-20220222200543937](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222200543937.png)

### characteristic equation特征方程法

![image-20220222200858760](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222200858760.png)

![image-20220222201019757](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222201019757.png)

![image-20220222201223696](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222201223696.png)

![image-20220222201407549](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222201407549.png)

**u和v通过代入初始条件来解得**

### guess and prove猜测并证明

![image-20220222201706278](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222201706278.png)

仍然是根据数学归纳法，先猜测T(n)=O(n)，即证明T(n)≤cn，证明这个**常数c足够大**即可，但事实证明发现不对，即T(n)=O(n)是不正确的

那么接下来猜测O(nlogn)*注意这里的对数底为2*

![image-20220222202026589](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222202026589.png)

证明的方法很简单，利用递推式，假设递推式右边的T≤猜想的复杂度成立，**看能不能推导出左边的T同样≤猜想的复杂度成立即可**

### recursion tree递归树

![image-20220222202549055](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222202549055.png)

![image-20220222202814773](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222202814773.png)

通过递归树计算代价时，是将要计算到的那一层的递归代价和从顶上到这一层产生的所有非递归代价之和。（**非递归代价在每一次递归中都会产生，而递归代价则被层层推到了最后一层**）

在第三层中n/4是不需要加入计算的，这个非递归代价是在第三层到第四层的过程中才产生的（回到原始递推式想），而此时计算的第三层的代价，因此不需要

因此根据递归树，最后一层是T(1)=0，而从上到下的所有非递归代价加起来就是nlogn（每层的非递归代价之和为n，共有logn层）

![image-20220222203521953](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222203521953.png)

**Θ(n^2^)用cn^2^来代替**

**中间递归代价可以不写**，由之前的递归树结论可以知道，中间的递归代价不参与代价的计算，**只需要写出最后一层的递归代价即可**

同时由前面的结论**最后一层没有非递归代价，只有递归代价**

而最下面一层的递归代价base case通常是常数，可以看作1或者常数c，所以**只要计算有多少个T(1)即可**。在这里每层是3倍，共log~4~n层，故为3^(log~4~n)^，利用换底公式得n^log~4~3^，故为cn^log~4~3^，可以用Θ来表示

![image-20220222204515065](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222204515065.png)

计算式的第二行，**对于公比小于1的等比数列求和，可以放缩成0~∞的求和**

右边是通过guess and prove来证明得到的T(n)≤O(n^2^)，对于常数c，不影响d，**只要让d的取值满足一定条件即可，这里的关键是3/16d<d**，如果不是小于，那么说明这个猜想是错误的

![image-20220222205605574](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222205605574.png)

对于分而治之的算法，很多最终都是变成这样的形式，==**即把一个规模为n的问题分成b个规模为n/c的问题，在这个分的过程会产生f(n)的非递归代价。共log~c~n层**==

**b叉树的非叶子结点都是非递归代价，叶子都是递归代价，总代价就是把所以结点求和**

![image-20220222210212465](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222210212465.png)

![image-20220222211018165](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222211018165.png)

关键指数critical exponent

## master theorem

![image-20220222210708782](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222210708782.png)

![image-20220223161924643](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223161924643.png)

![image-20220223163739799](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223163739799.png)

[对主定理(Master Theorem)的证明](https://www.cnblogs.com/erro/p/12249033.html)

ε的引入是为了保证case1中f(n)严格地比n^E^要小，case3中f(n)严格地比n^E^要大，此外δ的引入是保证f(n)不会比n^E^大太多，还是在多项式时间内的，而不是上升到指数，否则如果大的很多的话，T(n)=Θ(f(n))是不成立的

主定理中的3个case不能覆盖所有情况，**有些递推式是主定理无法解决的**

![image-20220222211916780](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222211916780.png)

![image-20220222212144311](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222212144311.png)

f(n)大，但不是大太多

![image-20220222212254403](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220222212254403.png)

幂次一定比对数增长快，因此找不到ε

