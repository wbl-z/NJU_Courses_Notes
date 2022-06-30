# Hash 哈希函数

## General Idea 基本思想
1. 键值映射：address = hash(key)
2. 提高查找速率

1) Sequention Search 线性搜索代价（顺序查找） O(n)
2) Binary Search 二元搜索代价（折半查找：前提是已经排序） O(log2n)
3) Hash Method 哈希映射搜索代价 O(1) 

- EX 1
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.0.1.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.0.2.png)

## Problem 痛点

散列表的搜索复杂度为常数复杂度，但空间浪费大，表中会有很多的空缺，而不能填满，同时有冲突的可能

选择一个碰撞率(冲突率)小的函数（根据装填因子&alpha;），n = 表中节点数，m = 表长
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.0.3.png)

## 1. Function Select 函数选择

### 1. 取余法

+ 特点：以关键码除以p的余数作为哈希地址。**在表的长度给定的情况下，p应当取比长度小的最大质数**

![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.1.1.png)![image-20211225162935410](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225162935410.png)

### 2. 平方法

+ 特点：对关键码平方后，按哈希表大小，取**中间的若干位（根据表长的位数来决定，如下，为3）**作为哈希地址。(**适于不知道全部关键码情况**)

![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.1.2.png)

### 3. 杂凑法

+ Hash(key)= ⎣ B*( A*key  mod  1 ) ⎦  (A、B均为常数，且0<A<1，B为整数)

   > 向下取整的运算称为Floor，用数学符号⌊⌋表示，与之相对的，向上取整的运算称为Ceiling，用数学符号⌈⌉表示。

+ 特点：**以关键码key乘以A，取其小数部分，然后再放大B倍并取整，作为哈希地址。**

+ 例：欲以学号最后两位作为地址，则哈希函数应为：
   H(k)=100*(0.01*k % 1 )
   其实也可以用法1实现： H(k)=k % 100

![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.1.3.png)

## 2. Collision Solution 碰撞处理
- **Load Factor 装填因子：**F(I)函数选择
- **开地址法：**
  1. 设计思路：有冲突时就去寻找下一个空的哈希地址，只要哈希表足够大，空的哈希地址总能找到，并将数据元素存入。
  2. 公式：(其中i递增即i++)![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.0.png)

### 1. Linear Probing 线性探测

当冲突时，就在这个位置的后面寻找空的格子，然后放入，即线性探测

- F(I) 选择**一次线性函数**，通常选择 F(I) = i
- hi(x) = ( Hash(x) + i ) % tableSize
- 若 H(x) = d，而 bucket d 已经被占据，则依序查找 **d+1, d+2, ..., m-1, 0, 1, 2, ..., d-1**，直到找到空的格子放入为止

- eg:
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.1.1.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.1.2.png)
- 平均搜索长度
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.1.3.png)

#### Problem 问题
1. Clustering Problem 堆积：几乎每次加入元素都碰撞
    ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.1.4.png)
2. 如果发生了删除，比如删除58，那么58所在位置会空了，**当搜索到空时，就停止了，不会往后再找**，因此35就找不到了![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.1.5.png)

#### Solution 解决办法
1. 没有，依赖哈希函数选择(根据不同输入有不同最佳函数)
    ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.1.5.png)
    
2. 可以不直接删除数据，而是作一个标记，表示这里以已经被删了。因此可以用两张表，一张为hashTable，另一张记录**曾经有没有过元素**；也可以在位置上增加标记

     - ![image-20211225164730689](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225164730689.png)
     - ![image-20211225165608773](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225165608773.png)

     查找实现C++：

     ![image-20211225165146070](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225165146070.png)![image-20211225164958783](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225164958783.png)

### 2. Quadratic Probing 平方探测

与线性探测一致，但通过二次函数，使得**探测的范围扩大**，可以**缓解**线性探测中的堆积问题

- F(I) 选择**二次函数**，通常选择 F(I) = **i^2^**
- hi(x) = ( Hash(x) + i^2^ ) % tableSize
- ![image-20211225165646157](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225165646157.png)

![image-20191228211412937](assets/image-20191228211412937.png)

eg![image-20211203173028636](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211203173028636.png)

一次递推式，那么事实上表达式为二次，如a~n~=a~n-1~+2n-1，最终a~n~=a~0~+f(n)，则f(n)为二次函数

**一般当数据量大于总容量的一半时就会进行扩容，避免冲突率过大**

### 3. Double Hashing 双重哈希(多重散列)

每次冲突的数据往后寻找位置的长度**c=hash2（k）都是不一样的**，两个hash函数能**很好地处理堆积问题**

- F(I) 为另一个哈希函数的倍数，即 **F(I) = hash2(x)*i**
- hi(x) = ( hash1(x) + hash2(x) * i ) % tableSize![image-20211203173623436](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211203173623436.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.3.1.png)

### 4. Rehashing 再散列
- 一遭遇**冲突就扩容**(再散列)，直到不发生冲突。

- 也于填充程度(填入项树/表大小)到达临界值时用于扩容（如当表项数 > 表的70% 时,可再散列。）

- 再散列的新表的长度应当为**2\*原表长的最小质数**（**乘2是为了满足扩容需求**）。如下，原表长为7，那么2\*7=14，取比14大的最小质数17，所以新表的长度应该为17

- ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.4.1.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.4.2.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.4.3.png)

- ![image-20211225170457587](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225170457587.png)

  把原来的散列表中的非null，且isactive==true（没有被删除）的重新计算，填入新的散列表中

### 5. Separate Chaining 分离链接法
- 表中每个槽(bucket)维护一个**链表**，注意链表中，**后加入的在前面**（这样插入节点时就**不需要遍历整个链表到最后**，而是直接在第一个就可以了）
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/5.2.5.1.png)
- 链表如果太长，效率就会极大降低
