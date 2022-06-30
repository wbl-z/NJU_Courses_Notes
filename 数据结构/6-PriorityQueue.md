# Priority Queue 优先队列

## 1. Priority Queue 优先队列

### Properties 属性
1. 每个元素含有值(value)或**优先级**(priority)
2. 查找(find)/删除(delelete)操作，在`最小/最大优先级队列(min/max priority queue)`均针对`优先级最小/最大`的元素

### Implementation 实现

#### 1. Linear List 线性表

+ **线性表：**
  1. 一个有限序列。
  2. 数据元素都是首尾相接的。

1. **insert 插入：**插入在**最右侧**，O(1)
2. **delete 删除：**查找最小优先级后删除，**O(n)**

## 2. Heaps 堆

### Definition 定义：max/min heap(最大堆/最小堆)
1. 是一棵**完全二叉树**\[**非常适合用数组表示**](complete binary tree)
2. **任意节点的值 >= or <= 其子节点的值**(树根往下为递减/递增)
3. 最大堆的顶点为最大值，最小堆的顶点为最小值。
- Max Heap
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/6.2.1.png)

- Min Heap
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/6.2.2.png)

### Properties 属性
1. int currentSize —— 堆的当前大小
2. int maxSize —— 堆的最大大小
3. T HeapNode —— 堆节点

### Operation(Methods) 操作

**核心**操作就是**数据进入操作和数据出去操作**

- int size() 取堆大小

- T Max() 查找最大元素

- MaxHeap< T > **insert**(T item) 插入节点 ——  **O(log~2~n)**（最坏情况就是遍历一遍**树高**）
  1) 插入元素放在完全二叉树的下一个位置，即堆的数组的最后
  2) 若为最大堆(最小堆)，而插入节点大于(小于)父节点，则插入元素与父节点**对调**（称为**上滤**），直到插入节点比父节点小（大）![image-20211226151237595](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226151237595.png)
  
  ![image-20211207081005212](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211207081005212.png)
  
- MaxHeap< T > **delete**(T item) `删除元素(删除根节点)`  **O(log~2~n)**，**最大堆删最大，最小堆删最小** 
  
  ——  **O(log~2~n)**
  
  1) 删除必删除根节点，将完全二叉树表示的**最后一个元素放到根节点，再做平衡**
  2) 平衡时选择**两个子节点中较大(较小)**的节点**上移**（相比于插入，要多比较一次，但复杂度最多还是遍历一遍树高）（**下滤**）
  
  ![image-20211207081311727](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211207081311727.png)
  
  ![image-20211226152125011](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226152125011.png)
  
- void initialize() 初始化 —— 自底向上排序

- MaxHeap< T > create(T[] items) 创建堆
  1. 按数据的初始顺序（即未排序）插入，先全部插入，再从底往上（**第[n/2]（向下取整）开始**）逐个**下滤**，**第i层最多要交换k-1-i次**，**复杂度O(n)**（最下面的需要交换的次数越少，如最后一行占了总节点数的一半，但已经不需要交换，所以只有很少的元素最多要交换一个树高）**<font color=#ff00>树中n~0~为【n/2】向上取整，n~2~+n~1~为[n/2]向下取整</font >**![image-20211207090754900](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211207090754900.png)
  
     ![image-20211207084344056](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211207084344056.png)
  
  2. 依次插入一个元素，插入就立即交换，但这里进行的是**上滤**，所以最后一行近一半的元素最多要进行一个树高的上滤，所以复杂度比上面更大，**复杂度O(nlogn)**
  
     (这与先排序，再逐个插入的代价相同)
  
     ![image-20211207084911895](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211207084911895.png)

#### MaxHeap< T > sort() 堆排序(最大堆)  **O(nlog~2~n)**

**先建堆，再重复执行删除操作**

![image-20211207090609773](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211207090609773.png)

1. 树根为最大，将树根和完全二叉树的最后一位交换（事实上就是删除操作）(此元素不再参与排序，移出树，也可以放在原来的最后一位的位置，这样数组中的元素最终是按递增/递减顺序排好的)

2. 恢复最大堆（删除操作使用下滤，把最上面的元素往下移动）(较大元素上移，较小的下移)，然后回去执行1.，直到所有元素都排序过

3. 时间复杂度：**初始化 + 调整 = O(nlog~2~n)**

4. 空间复杂度**O(1)**，只利用了原本的空间

5. 堆排序是**不稳定**的

   > 存在多个具有**相同的关键字**的记录，若经过排序，这些记录的相对次序保持不变，即在原序列中，r[i]=r[j]，且r[i]在r[j]之前，而在排序后的序列中，r[i]仍在r[j]之前，则称这种排序算法是稳定的；否则称为不稳定的。
   
   ![image-20211226153723188](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226153723188.png)![image-20211226153730923](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226153730923.png)![image-20211226153736271](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226153736271.png)

### Algorithm Analysis 算法分析

**选择第k大的数的问题：**

- n个元素寻找第 k 大的元素
1. n 个数据放入数组，`选择排序`，取第 k 个 => 复杂度 O(n^2^)
2. 读入 k 个元素，按递减排序，其余元素每个与最后一个元素比较，若插入则重新排序，全部插入后最后一个元素就是第 k 大的元素 => 复杂度 O(n^2^)
3. n 个元素建`最大堆`，执行 **k 次 delete**，根节点为第 k 大元素 => 复杂度 O(n+klogn)
4. **前k 个元素建`最小堆`**，其余元素与根节点(此时为第 k 大)比较，**大于则替换根节点并调整**，全部插入后根节点就是第 k 大的元素 => 复杂度 O(nlogn)

