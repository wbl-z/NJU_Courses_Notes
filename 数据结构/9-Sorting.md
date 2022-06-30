# Sorting 排序算法

## 0. General Idea
- **排序：**将元素(基本数值或是可比较对象)按照其关键码小往大(非递减)或大往小(非递增)次序重新排列
- **key 关键码：**由原数据(Data)计算得出或标记(tag)作为比较前后顺序的依据

### Category 分类
- **内排序：**内存中 n 个对象的排序
1. 插入排序
2. 交换排序
3. 选择排序
4. 归并排序
5. 基数排序

- **外排序：**数据量较大，或数据牵涉磁盘与内存间的移动

### Stability 稳定性
- **稳定的：**关键码相同的元素在排序后前后次序不变
- **不稳定的：**相反

### Algorithm Analysis 算法分析
- **Time Complexity 时间开销：**比较次数、数据移动次数
  + 比较总次数 KCN + 移动次数 RMN
- **Space Complexity 空间开销：**所需附加空间
- **原数据表定义**
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.0.1.png)

## 1. Insert Sort 插入排序

### 0. Main Idea 主要思想
- 将 Vn 插入以排序好的 0 ~ V(n-1)里面

### 1. Straight Insert Sort 直接插入排序
- 将第 i 个元素依序放到 0 ~ i-1 个元素中该放的位置(i = 1 ~ n-1)
- `稳定的`

#### 步骤：n 个数排序，下标为 0 ~ n-1
1. 选择数列中第 i 个数(i = 1 ~ n-1)为 num
2. 将 num 往前比较直到遇到 <= num 的数，插入在此数后面
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.1.1.gif)

```java
public static void insertionSort( Comparable [ ] a ){ 
    int j;
    for ( int p = 1; p < a.length; p++ ){ 
        Comparable tmp = a[ p ];
        for ( j = p; j > 0 && tmp.compareTo( a[ j – 1 ] ) < 0; j-- )
            a[ j ] = a[ j – 1 ];
        a[ j ] = tmp;
    }
} 
```

#### Algorithm Analysis 算法分析

1. 比较次数 KCN = sum(2~n){(i+1)/2} = O(n^2)
2. 交换次数 RMN <= sum(2~n){(i+3)/2} = O(n^2)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.1.4.png)

### 2. Binary Insert Sort 折半插入排序(二分法插入排序)
- 每次只与区间中最中间元素比较
- `稳定的`

#### 步骤：n 个数排序，下标为 0 ~ n-1
1. 将已排好序列作为初始`区间`，分成左右两份
2. 将欲插入元素 i 与中间元素 n(mid) 比较，i <= n则选左边，否则选右边
3. 选择区间作为下一次比较的区间，重复执行1,2
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.1.2.png)

```c++
template <class Type> void BinaryInsertSort( datalist<Type> &list){ 
    for (int i=1; i<list.currentSize; i++) 
        BinaryInsert(list, i);
}

template <class Type> void BinaryInsert( datalist<Type> &list, int i){ 
    int left=0, Right=i-1;
    Element<Type>temp=list.Vector[i];
    while (left<=Right){ 
        int middle=(left+Right)/2;
        if (temp.getkey( )<list.Vector[middle].getkey( ))
            Right=middle-1;
        else 
            left=middle+1;
    }
    
    for (int k=i-1; k>=left ; k--) 
        list.Vector[k+1]=list.Vector[k];
    list.Vector[left]=temp;
}g
```

#### Algorithm Analysis 算法分析

1. 比较次数与总个树有关
2. 设 n = 2^k，则每次插入需要比较 KCNi = floor(log2(i)) + 1次，总共需要 sum(i=1~n-1){KCNi} = (log2(n)-1)n + 1 = O(nlgn)

- 复杂度：O(nlgn)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.1.5.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.1.6.png)

### 3. 链表插入排序
- 直接排序以链表实现(1.使用数组实现)

### 4. Shell Sort 希尔排序(Diminishing-increment Sort 缩小增量排序)
- 使用增量(gap < n)分组，每组使用直接排序或其他排序
- `不稳定`

#### 步骤：n 个数排序，下标为 0 ~ n-1
1. 取一增量(gap < n)，对每组使用**直接插入排序**(`因为是有序的数组，所以使用直接插入排序的复杂度更低，能充分利用前面的gap的结果`)或其他方法进行排序
2. 减少增量（分的组减少，但每组记录增多），递归执行第一步，直到 gap = 1
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.1.3.png)

```java
public static void shellsort( Comparable [ ] a ){ 
    for ( int gap = a.length / 2; gap > 0; gap /= 2 )
        for ( int i = gap; i < a.length; i++ ){ 
            Comparable tmp = a[ i ];
            int j = i;
            for ( ; j >= gap && tmp.compareTo( a[j- gap]) < 0 ; j -= gap)
                a[ j ] = a[ j – gap ];
            a[ j ] = tmp;
        }
}
```

#### Algorithm Analysis 算法分析

- 与 gap 有关，最佳增量序列未知
- KCN 和 RMN 大约为 n^1.3^ = O(n^1.3^)

## 2. Exchange Sort 交换排序
- 不断交换反序的数对，直到任意两树都为顺序

### 1. Bubble Sort 冒泡排序
- 将数列中的最大数依序冒泡到列尾(或是列头)
- `稳定的`

#### 步骤：n 个数排序，下标为 0 ~ n-1
1. 比较 n-1 趟
2. 第 i 趟(i = 0 ~ n-2)依序比较相邻的两个元素 [j, j+1], j = 0 ~ n-2-i
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.2.1.gif)

```c++
template<class Type> void BubbleSort( datalist<Type> & list){ 
    int pass=1;
    int exchange=1;
    while (pass<list.CurrentSize &&exchange){ 
        BubbleExchange(list, pass, exchange); pass++;
    }
}

template<class Type> void BubbleExchange(datalist<Type> &list, const
int i, int & exchange){ 
    exchange=0;
    for (int j=list.CurrentSize-1; j>=i; j--)
        if (list.Vector[j-1].getkey( )>list.Vector[j].getkey( )){ 
            swap( list.Vector[j-1], list.Vector[j] );
            exchange=1;
        }
    
}
```

#### Algorithm Analysis 算法分析

- 复杂度：O(n^2)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.2.2.png)

### 2. Quick Sort 快速排序
- 取某一数，依关键码将其余的数分两堆，对其余两堆再递归进行一次快速排序
- `不稳定`

#### 步骤：n 个数排序，下标为 0 ~ n-1
1. 取任意一个数(通常取中间 m)，i, j分别从左右往中间移动
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.2.8.png)

2. 若 num[i] <= m 且 num[j] >= m，则 i++, j--

   若 num[i] >m 且 num[j] < m，则 num[i], num[j] 交换并且 i++, j--

   若 num[i] > m 而 num[j] >= m，则 j--

   若 num[i] <= m 而 num[j] < m，则 i++
5. 直到 i == j 则将所选数字放到中间位置 i 以左为左边区块，j 以右为右边区块
6. 分别对两侧区块递归执行快速排序（**两边的快排是可以同时进行的**）
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.2.3.gif)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.2.4.png)

```java
private static void quicksort( Comparable [ ] a, int left, int right ){
    if( left + CUTOFF <= right ){ 
        Comparable pivot = median3( a, left, right );
        int i = left, j = right – 1;
        for( ; ; ){ 
            while( a[ ++i ] . comparaTo( pivot ) < 0 ) { }
            while( a[ --j ] . compareTo( pivot ) > 0 ) { }
            if( i < j )
                swapReferences( a, i, j );
            else 
                break;
        }
        swapReferences( a, i, right – 1 );
        quicksort( a, left, i – 1 );
        quicksort( a, i + 1, right );
    }else
        insertionSort( a, left, right );
    
}
```

#### Algorithm Analysis 算法分析

- **Time Complexity 时间复杂度：**最坏 O(n^2)，平均 O(nlgn)（第一次就复杂度n，第二次分成两边快排，两个合起来复杂度n，同理第三次，分成4个快排，合起来是复杂度n，共需要log~n~轮，所以平均复杂度为nlog~n~）
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.2.5.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.2.6.png)

- **Space Complexity 空间复杂度**
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.2.7.png)

## 3. Select Sort 选择排序

### 1. Straight Select Sort 直接选择排序

#### 步骤：n 个数排序，下标为 0 ~ n-1
1. 第 i(i = 0 ~ n-1) 趟，从 n 个数中选取最小(最大也可)的值 min，顺序置于列头(列尾也可)
2. 将 min 的值与 i 位置的值交换
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.3.1.gif)		

```c++
template <class Type> void SelectSort(datalist<Type> &list){ 
    for ( int i=0; i<list.CurrentSize-1; i++)
        SelectExchange(list, i);
}

template <class Type> void 
    SelectExchange( datalist<Type> &list, const int i){ 
    int k=i;
    for ( int j=i+1; j<list.CurrentSize; j++)
        if (list.Vector[j].getkey( )<list.Vector[k].getkey( )) 
            k=j;
    if ( k!=i) 
        Swap(list.Vactor[i], list.Vector[k]);
}
```

#### Algorithm Analysis 算法分析

- 复杂度：O(n^2)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.3.2.png)

### 2. 锦标赛排序
- `稳定的`

#### 步骤：n 个数排序，下标为 0 ~ n-1
1. n 个对象两两比较，挑出 ceil(n/2) 个比较小(比较大)的对象
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.3.4.png)

2. 不断两两比较直到找出最小值，保留此最小值，对剩下的对象再做一次，直到找出 n-1 个最小值
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.3.3.png)

#### Algorithm Analysis 算法分析

- 复杂度：O(nlgn)
- 需要 n-1 个**附加空间**用于建树·（空间复杂度高，相比于堆排序一般不用）
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.3.5.png)

### 3. 堆排序
- 小到大排序(递增)使用最大堆(Max Heap)
- 大到小排序(递减)使用最小堆(Min Heap)
- `不稳定`

#### 步骤：n 个数排序，下标为 0 ~ n-1
1. 原数据 -> 完全二叉树 -> 调整为最大堆(最小堆)
2. 树根下降(或是直接与最后一个位置的数对换)到最后一个位置后移除
3. 恢复(调整)下降后不满足最大堆的部分
4. 递归2,3步直到所有数字都被排序
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.3.6.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.3.7.png)
- Result: 8, 16, 21, 25*, 25, 49

```java
public static void heapsort( Comparable [ ] a ){ 
    for( int i = a.length / 2; i >= 0; i-- )
        percDown( a, i, a.length );
    for( int i = a.length – 1; i > 0; i-- ){ 
        swapReferences( a, 0, i );
        percDown( a, 0, i);
    }
}

private static int leftChild( int i ){ 
    return 2 * i + 1;
}
```

#### Algorithm Analysis 算法分析

- 建堆：O(n)
- 排序：O(nlgn)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.3.8.png)

## 4. Merge Sort 归并排序
- 归并：合并两个有序列表

  （假设把列表分成两半，两边是已经排好序的，那么现在的问题就是如何把已经排好序的两边合并成一个排好序的，**递归**）

  **分而治之思想**
1. i, j 分别指向两个列表的第一个元素
2. 取出 i, j 中较小的元素，并且向后移动一格 i++ or j++
3. 一个列表取完则输出另一个列表的剩余对象

### 1. 迭代的归并排序（自顶向下方法，与递归相反）
- `稳定的`

#### 步骤：n 个数排序，下标为 0 ~ n-1
1. n 个长为 1 的数组各自归并
2. floor(n/2) + 1 个长为 2 的数组各自归并...
4. 直到所有数都被归并为同一个数组
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.4.1.png)

```c++
template <class Type> void MergeSort(datalist <Type> & list){ 
    datalist <Type> tempList(list.MaxSize);
    int len=1;
    while (len<list.CurrentSize){ 
        MergePass(list, tempList, len); 
        len *=2 ;
        if (len >= list.CurrentSize){ 
            for (int i=0 ; i< list.CurrentSize; i++)
                list.Vector[i]=tempList.Vector[i];
        }else {
            MergePass (tempList, list, len); 
            len*=2;
        }
    }
    delete[ ]tempList;
}


template <class Type> void MergePass( datalist<Type> & initList, datalist
<Type> & mergedList, const int len){ 
    int i=0;
    while (i+2*len<=initList.CurrentSize-1){ 
        merge( initList, mergedList, i, i+len-1, i+2*len-1);
        i+=2*len;
    }
    if (i+len <= initList.CurrentSize-1)
        merge( initList, mergedList, i, i+len-1, initList.CurrentSize-1);
    else 
        for ( int j=i ; j<= initList.CurrentSize; j++)
            mergedList.Vector[j]=initList.Vector[j];
}

template<class Type> void merge(datalist<Type> & initList, datalist<Type> & mergedList, const int l, const int m, const int n){ 
    int i=l, j=m+1, k=1;
    while ( i<=m && j<=n )
        if (initList.Vector[i].getkey( )<initList.Vector[j].getkey( )){ 
            mergedList.Vector[k]=initList.Vector[i]; i++;k++;
        }else {
            mergedList.Vector[k]=initList.Vector[j]; j++; k++;
        }
    if ( i<=m)
        for (int n1=k, n2=i; n1<=n && n2<=m; n1++, n2++)
            mergedList.Vector[n1]=initList.Vector[n2];
    else
        for (int n1=k, n2=j; n1<=n && n2<=n; n1++, n2++)
            mergedList.Vector[n1]=initList.Vector[n2];
}
```

#### Algorithm Analysis 算法分析

- 归并 lgn 趟，趟次比较 n 次，复杂度为 O(nlgn)

### 2. 递归的表归并排序

#### 步骤：n 个数排序，下标为 0 ~ n-1
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.4.2.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.4.3.png)

```java
public static void mergeSort( Comparable [ ] a ){ 
    Comparable [ ] tmpArray = new Comparable[ a.length ];
    mergeSort( a, tmpArray, 0, a.length – 1 );
}

private static void mergeSort( Comparable [ ] a, Comparable [ ] tmpArray,
int left, int right ){ 
    if( left < right ){ 
        int center = ( left + right ) / 2;
        mergeSort( a, tmparray, left, center );
        mergeSort( a, tmpArray, center + 1, right );
        merge( a, tmpArray, left, center + 1, right );
    }
}

private static void merge( Comparable [ ] a, Comparable [ ] tmpArray,
int leftPos, int rightPos, int rightEnd ){ 
    int leftEnd = rightPos – 1;
    int tmpPos = leftPos;
    int numElements = rightEnd – leftPos + 1;
    while( leftPos <= leftEnd && rightPos <= rightEnd )
        if( a[ leftPos ].compareTo( a[ rightPos ] ) <= 0 )
            tmpArray[ tmpPos++ ] = a[ leftPos++ ];
    else 
        tmpArray[ tmpPos++ ] = a[ rightPos++ ];
    while( leftPos <= leftEnd )
        tmpArray[ tmpPos++ ] = a[ leftPos++ ];
    while( rightpos <= rightEnd)
        tmpArray[ tmpPos++] = a[ rightpos++ ];
    for( int i = 0; i < numElements; i++, rightEnd-- )
        a[ rightEnd ] = tmpArray[ rightEnd ];

} 
```

## 5. 内排序总结

![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.5.1.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/9.5.2.png)

![image-20211224173715304](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211224173715304.png)

​	
