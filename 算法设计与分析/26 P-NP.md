## P, NP, and NP-Complete

![image-20220525140743423](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525140743423.png)

### What is a decision problem?

![image-20220525140805234](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525140805234.png)

- 优化问题：需要回答具体值
- 决策性问题：需要回答 YES / NO
- **两个问题从 P/NP 角度来看难度一样**。但渐进复杂度不一样，优化问题比决策性问题会更复杂

![image-20220525141233194](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525141233194.png)

#### example：最大团问题的两个问题

![image-20220525141403034](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525141403034.png)

#### 经典的决策性问题

![image-20220525142349131](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525142349131.png)

![image-20220525142356767](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525142356767.png)

![image-20220525142404664](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525142404664.png)

### When we say a problem is in P, what do we mean exactly?

![image-20220525142429556](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525142429556.png)

输入以二进制表示的位数是输入的规模，如果算法的最坏复杂度是输入规模的多项式，那么是多项式算法

![image-20220525142806122](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525142806122.png)

- P 问题的范围很大，对于 P 问题，不一定能在可接受的范围内解决，比如复杂度是 n 的十亿次方。**但不是 P 问题的问题，代码一定的非常昂贵甚至无法解决的**
- 多项式有很好的**闭包** *closure* 性质，加减乘后仍然是多项式

### What do we mean by “NP”?

NP的英文全称是**Non-deterministic** Polynomial的问题，即多项式复杂程度的**非确定性问题。**

P类问题：可以在多项式时间内**求出问题的解**的问题；

NP问题： 可以在多项式时间内**验证一个正确的解**的问题；

> 下面证明，如果一个问题是P类问题，它一定是NP问题；
>
> 证明：
>
> 假设A是P类问题，则它可以多项式时间内求解； 现在我们任意给定一个猜测解b，我们可以先在多项式时间内解出A的真实解a,以O(1)时间比较a和b是否相等；如此，就在多项式时间内验证了b是否是正确的解，也就满足NP问题的条件.QED

![image-20220525143852163](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525143852163.png)

![image-20220525144815651](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525144815651.png)

非确定性算法：第一步：随机猜一个答案；第二步：验证答案是否正确

![image-20220525145131863](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525145131863.png)

![image-20220525145256385](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525145256385.png)

因此这里的图着色问题在给定的答案，能够在多项式时间内验证是不是 YES，所以它是一个 NP 问题

### P & NP

![image-20220525145550031](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525145550031.png)

NP 问题可能比较难，因为验证结果是否正确就已经是多项式时间了，而解决问题可能远远大于多项式时间

![image-20220525145751414](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525145751414.png)

![image-20220525150347334](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525150347334.png)

### 如何证明一个问题是 NP 问题

![image-20220525150148367](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525150148367.png)

#### example

![image-20220525150225482](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525150225482.png)

![image-20220525150304557](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525150304557.png)

合取范式的可满足性问题

### NPC

![image-20220525150628929](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525150628929.png)

多项式规约

将 E 问题的输入转换成已经可以解决的问题 Q 的输入，根据 Q 的输出就能知道 E 的答案，**即找到间接解决 E 的方法**

如果 T 和 Q 都是多项式时间的，那么整个绿框即 E 也是多项式时间的【多项式的闭包】

**多项式规约要求：**

- T 可以在多项式时间内解决

- x 是 E 的 YES input -> T(x) 是 Q 的 YES input

- x 是 E 的 NO input -> T(x) 是 Q 的 NO input

  这条通常**证明其逆否命题**，即 T(x) 是 Q 的 YES input -> x 是 E 的 YES input

**T 要能处理所有 E 的 input x，但映射到的 T(x) 不一定是 Q 的所有输入。**

对于问题 E 和 Q，Q 问题应该更难，至少不比 E 简单。否则不能解决问题 E，正如集合关系，满足子集 E 的肯定满足集合 Q，但满足集合 Q 的不一定满足子集 E

![image-20220525152403449](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525152403449.png)

#### example

![image-20220525151631444](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525151631444.png)

#### definition

![image-20220525152515929](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525152515929.png)

NP 难问题，对于所有的 NP 问题，如果都能在多项式时间内规约到 Q，那么 Q 就是一个 NP 难问题。

NP 完全问题，如果一个问题既是 NP 问题，又是 NP 难问题，那么是 NP 完全问题，**NPC问题代表了 NP 问题中最难的问题。相反，NPC问题代表了 NP 难问题中最容易的问题**

### 难度分类的作用

![image-20220525152805419](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220525152805419.png)

可以用来证明许多没有已知多项式时间算法的问题在计算上是相关的。

告诉我们问题之间的联系，一旦为某些问题找到多项式时间的答案，那么其他问题也就找到了

