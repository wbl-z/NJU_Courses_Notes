Disjoint Set 并查集

## 1. Equivalence Class 等价类(Online Equivalence Class 等价类划分)
1. 自反性：aRa
2. 对称性：aRb => bRa
3. 传递性：aRb, bRc => aRc

- Equivalence Relationship 等价关系 => Online Equivalence Class 等价类划分(A/R)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/7.1.1.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/7.1.2.png)

### Operation 操作
1. combine/union(a, b)：合并(union)a, b元素的等价类
2. find(e)：查找含有元素e的**等价类**

![image-20211210162135107](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210162135107.png)

### Implementation 实现
1.  Tree Representation(Forest)**树**实现：**一棵树代表一个等价类，等价类划分为树的集合(即森林)**
2. **父节点指针数组**(Parent)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/7.1.3.png)

- union(a, b) 并集：将一个树(等价类)作为**另一个树的根节点**的子元素
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/7.1.4.png)

#### Time Complexity 时间复杂度
1. find(x) 查找操作：**O(h)**，h 为高度
2. union(a, b) 合并操作：&theta;(1)，**常数复杂度**

#### Problem 问题
- 单边链的查找表现不好
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/7.1.5.png)

#### Solution 解决方法
1. **Weight Rule** ：让节点多的树作节点少的树的父节点
    ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/7.1.6.png)![image-20211210162647453](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210162647453.png)
    
    ![image-20211210162834802](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210162834802.png)![image-20211210162843201](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210162843201.png)

2. **Height Rule** ：让较高的树作较矮的树的父节点（这样树高不会增加，只有当两个树的树高一样是，树高才会加1）

   根结点中放**负数**，而且是代表高度。Parent数组中根节点位置保存树的高度
   ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/7.1.7.png)

   当树高小的挂到树高大的树上去时，树高不必更新，因为树高没变，只需要把矮的树的parent改成高的树即可。

   当两者树高相等时，需要更新树高，如下--，因为这里用负数记录树高，所以要-1

   ![image-20211210163208676](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210163208676.png)![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/7.1.8.png)

3. **Path Compression 路径压缩**：查找目标到根的路径上所有节点全部变成一层节点

   先根据e找到根节点j，然后**再遍历一遍**，把路径上的所以节点的父节点都改成树根，这样对于e，只有**第一次查找时复杂度很高，但在之后的复杂度都很低**![image-20211210164152942](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210164152942.png)![image-20211210164359882](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210164359882.png)![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/7.1.9.png)

