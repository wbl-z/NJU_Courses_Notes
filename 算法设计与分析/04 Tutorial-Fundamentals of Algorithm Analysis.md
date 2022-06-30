# 04 Tutorial-Fundamentals of Algorithm Analysis

![image-20220223200145204](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223200145204.png)



一般来说随着输入规模的变大，最坏时间复杂度会升高，但有些算法中不是单调增的

![image-20220223200320232](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223200320232.png)

![image-20220223200430284](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223200430284.png)

![image-20220223200700240](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223200700240.png)

并不是任意的两个函数都存在5种关系中的某种，如上面的例子，n趋向无穷时极限不存在

![image-20220223200911426](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223200911426.png)

![image-20220223201119273](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223201119273.png)

## find maximum subsequence sum

![image-20220223201646727](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223201646727.png)

![image-20220223202446793](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223202446793.png)

![image-20220223202503004](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223202503004.png)

T(n)=2T(n/2)+Θ(n)，由master theorem符合case2，因此为Θ(nlogn)

![image-20220223203133102](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223203133102.png)

**online algorithm**

![image-20220223203631486](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220223203631486.png)

> PS：在线算法(online algorithm)和离线(offline algorithm)算法，离线算法也就是知道了所有的输入，根据某些条件来选取最佳策略，而在线算法就是无法预知到后面的输入，只能按照**目前的状况来做出下一步的最好决策**，**在线算法追求的是与离线算法一样的好结果**

> ## 解法五 - 数学分析
>
> ### 思路
>
> 我们来通过数学分析来看一下这个题目。
>
> 我们定义函数 S(i) ，它的功能是计算以 0（包括 0）开始加到 i（包括 i）的值。
>
> **那么 S(j) - S(i - 1) 就等于 从 i 开始（包括 i）加到 j（包括 j）的值。**
>
> 我们进一步分析，实际上我们只需要遍历一次计算出所有的 S(i), 其中 i 等于 0,1,2….,n-1。
> **然后我们再减去之前的 S(k),其中 k 等于 0，1，i - 1，中的最小值即可。 因此我们需要**
> **用一个变量来维护这个最小值，还需要一个变量维护最大值。**
>
> 这种算法的时间复杂度 **O(N)**, 空间复杂度为 O(1)。
>
> 其实很多题目，都有这样的思想， 比如之前的《每日一题 - 电梯问题》。

## Towers of Hanoi

![image-20220224090302022](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224090302022.png)

## Cutting the plane

![image-20220224090541277](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224090541277.png)

![image-20220224090548207](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224090548207.png)

## Number of Valid Strings

![image-20220224091126244](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224091126244.png)

![image-20220224091136866](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224091136866.png)

利用**分治思想**，**将大问题n化解为规模为n-1的小问题或n-1，n-2的问题**，找到递推方程式求解

![image-20220224091655656](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224091655656.png)

## Matrix Multiplication

![image-20220224092333533](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224092333533.png)

![image-20220224092344736](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224092344736.png)

![image-20220224092413836](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224092413836.png)

![image-20220224092427831](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224092427831.png)

Adding sub-matrices时要加4*(n/2)^2^次，故为Θ(n^2^)

![image-20220224092733529](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224092733529.png)

**只需要计算7次乘法，故log~2~7，从而降低了复杂度**。这是目前计算矩阵乘法的**最快算法**

## guess and prove

![image-20220224093446414](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224093446414.png)

guess需要一定的技巧

### special case

![image-20220224093923131](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224093923131.png)

![image-20220224093932818](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220224093932818.png)

在猜测T(n)<kn时最后相比于猜想式子多了一个常数c，**因此我们在猜想时也加上常数b**，即T(n)<kn-b从而最终成功证明。则T(n)=O(n)

