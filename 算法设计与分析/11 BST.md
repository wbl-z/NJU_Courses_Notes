# BST

![image-20220325134137792](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325134137792.png)

- 动态集合即这个集合是**动态变化**的，可以插入删除，而不是前面如排序，选择那样给定n个就不变的
- **关注key**，且一般key是不一样，且能两两比较，即全序关系（*集合内任何一对元素在在这个关系下都是相互可比较的*）
- 而不关注卫星数据，即伴随key的一些其他数据

![image-20220325134701642](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325134701642.png)

后继successor即在所有比x大的元素中最小的就是x的直接后继

![image-20220325135006654](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325135006654.png)

选择关注元素之间的偏序关系，查找关注元素本身的值

![image-20220325135200104](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325135200104.png)

- 二分查找用于排序好的静态集合O(logn)
  - 如找到N的算术平方根，即在0~N之间找一个数即可，采用二分查找
  - ![image-20220325135516355](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325135516355.png)
    对于严格增加和减少的单峰集合，只要二分查找即可找到最大的值![image-20220325135905627](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325135905627.png)
  - 如果上面的题目不是严格的，即weakly，先是非减，再非增的，那么上面的方法就不适用了，可能会有相等的情况，此时可以进行改进，即当相等时就对左右两边递归找max，因为无法确定是左边还是右边![image-20220325140048643](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325140048643.png)
- BST用于动态集合

## BST

![image-20220325140213499](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325140213499.png)

节点**大于左子树**上的所有元素，**不大于(<或=)右子树**上的所有元素

**给BST增加黑色的节点(external node)（哨兵）（哨兵个数为树的节点数+1）**，其key为空，这样当查找到哨兵时就知道要查找的这个元素不在数里面

对于BST可以通过一次**中序遍历**即可输出排序好的集合

![image-20220325141218854](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325141218854.png)

对于一些连通的内部节点（这里的内部节点即除掉external node后的节点）可以称为node gruop，而如果一个subtree的root的父节点在node group中，但subtree不在，那么就称这个subtree为**principal subtree**，**后续在让二叉树平衡的操作时即为操纵这些principal subtree旋转来实现**

![image-20220325141659772](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325141659772.png)

![image-20220325141720998](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325141720998.png)

最早的平衡二叉搜索树是AVL树，由于要求左右子树的高度差不超过1，这样的绝对条件使得AVL树的维护较复杂。

AVL树可以看作是对平衡的**绝对定义的树**。
红黑树是一种**相对平衡**的二叉搜索树

## 红黑树RBT

### 定义

![image-20220325142109871](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325142109871.png)

红色节点不能有红色的孩子，但黑色节点可以有黑色的孩子

**平衡控制条件**：任意选择一个节点，那么这个节点往下到所有的外部节点的**黑色路径长度是一样**的（**黑色路径长度即路径上黑色节点的数目-1**）

**ARB tree即根节点是红色的，其他定义一样**

![image-20220325142657461](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325142657461.png)

![image-20220325142753777](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325142753777.png)

没有ARB~0~，因为ARB的root必须是red，所以ARB~0~至少有一个黑色节点，那么==？？==

RB~1~只有4种情况

### 递归定义

![image-20220325143236414](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325143236414.png)

![image-20220325143250748](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325143250748.png)

![image-20220325143339686](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325143339686.png)

采用更加清晰的画法，**如果是子节点是黑色节点那么level+1往下画，如果子节点是红色节点，那么平着画和父节点处于同一level**，这样可以清楚地看到black height是2

### 性质

![image-20220325143727442](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325143727442.png)

对于h的RBT，红黑交替时**内部节点**数目最多，全是黑色时**内部节点**数目最少

- 对于任意的**黑色节点**，**其高度最多是其黑色高度的两倍**，如黑-红-黑-红-黑，height = 4，black height = 2；
- 对于**红色节点则不一定**，如红-黑-红-黑，那么height = 3，black height = 1

![image-20220325144055207](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325144055207.png)

即用递归定义证明了红黑树中黑色高度**意味着**所有黑色外部节点到root的黑色路径长度是一样的

![image-20220325145215535](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325145215535.png)

对于高度为h的RBT，那么内部节点数量至少为2^h^-1，即全部为黑色，但对于n个节点，其中不一定全是黑色，所以2^h^-1≤n,h≤lg(n+1)，即**黑色高度最多是lg(n+1)**。而由性质可知，根节点的高度最多是黑色高度的两倍，**所以RBT的高度最多是2lg(n+1)**

因此可以看到对于红黑树，**其查找复杂度仍然是log(n)级别的**

![image-20220325150548244](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325150548244.png)

插入：最坏需要查找Θ(logn)，然后还要进行修复，修复最坏情况下需要O(logn)即从最底层一直修复到最上层

删除操作同理

## example

​	![image-20220321102339920](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220321102339920.png)

- 配对消除的方法，只需要Θ(n)
- 排序看中位数，一定是重元素，O(nlogn)

![image-20220325152613817](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325152613817.png)

logn一定是二分法

取中间元素x，和最左边L和最右边R两个元素比较：如果x<L,x<R，那么说明max在L和x之间，递归；如果x>L,x>R，那么说明max在x和R之间递归

![image-20220325152842937](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325152842937.png)

:star:用*x(x+1)/2=n*计算出x，故复杂度为**根号n**

![image-20220325153540414](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220325153540414.png)



![image-20220321102339920](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220321102339920.png)

- 配对消除的方法，只需要Θ(n)
- 排序看中位数，一定是重元素，O(nlogn)

![image-20220321102840847](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220321102840847.png)

![image-20220321103143071](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220321103143071.png)
