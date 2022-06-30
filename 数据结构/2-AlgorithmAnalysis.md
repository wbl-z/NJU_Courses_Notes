# Algorithm Analysis 算法分析

## Basic Idea
- **Algorithm 算法：**描述解決问题的具体指令
- **Algorithm Analysis 算法分析：**计算算法需要耗费的`内存大小`与`运行时间`

## Target 算法目标
- **Space Complexity 空间复杂度：**算法需要的`内存大小`
- **Time Complexity 时间复杂度：**算法需要运行的`时间`

## Space Complexity 空间复杂度

+ **组成：**

  1. Instruction Space 程序大小
  2. Data Space 数据大小(算法所需变量、常量空间大小)
  3. Enviorment Stack Space 环境空间(堆、栈使用空间)

+ **分类：**

  1. 固定部分：指令、固定长度的变量、常量储存空间
  2. 可改变部分：变量、动态分配空间、递归栈储存空间
  3. 空间复杂度的的计算**主要针对可改变的空间**

+ **例子：**

  ```java
  public static float Rsum(float[] a, int n){ 
      if ( n>0 )
          return Rsum(a, n-1) + a[n-1];
      return 0;
  }
  ```

  - 递归栈空间：

    参数：a(2B), n(2B)

    地址：2B

    深度：n+1（从n到0，共n+1层）

    S(n) = 6(n+1)

- **Keys:** 计算方法所使用的变量数量 * 占用空间

## Time Complexity 时间复杂度
+ **T(p)=compile time+run time**

  1. Compile time 编译时间
  2. run time 运行时间(operation counts)
  3. 运行时间取决于实例特性(instance characteristics)

+ **平均、最好、最坏复杂度：**

  1. 平均复杂度：把每种情况下的复杂度加起来，然后除以情况的个数，所得的值就是平均复杂度，类似于数学上的均值。

  2. 最好时间复杂度：在最理想的情况下，执行这段代码的时间复杂度。

  3. 最坏时间复杂度：在最不理想，运气最坏的时候，执行这段代码的时间复杂度。

  4. 均摊时间复杂度：**绝大部分是低级别的复杂度，个别情况是高级别复杂度，且这些操作之间存在前后连贯的时序关系。**这个时候，我们就可以将这一组操作放在一块儿分析，看是否能将较高时间复杂度那次操作的耗时，平摊到其他那些时间复杂度比较低的操作上。而且，**在能够应用均摊时间复杂度分析的场合，一般均摊时间复杂度就等于最好情况时间复杂度。**

     如插入数组，当空间不够时数组扩大2倍，每一次O(n)时间复杂度的操作之后，还有n-1次的O(1)时间复杂度操作。所以我们可以把O(n)时间分摊到O(1)中，这样最终的均摊时间复杂度还是O(1)。

+ **渐进表示法(Asymptotic Notation)(O, &Omega;,&theta;)：**

  1. 形容**很大的实例特性**的空间与时间复杂度。

  2. 大O表示法(Big Oh Notation(O))： **表示算法上界**，f(x)以g(x)为上界，**描述算法的最坏复杂度**，没有明确下界的时候，使用大O表示法。对所有n, n>=n0，如果f(n)<=cg(n)，则f(n)=O(g(n))。例如：f(n)=3n+2，n>=2、3n+2<=3n+n=4n，故f(n)=O(n)。

     ![大O](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/大O)

  3. 大&Omega;表示法(Omega Notation(&Omega;))：**表示算法下界**，f(x)以g(x)为下界，**用与描述算法的最优复杂度**，没有明确的上界的时候，使用大Ω表示法。对所有n, n>=n0，如果f(n)>=cg(n)，则f(n)=O(g(n))。

     ![大Omega ](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/大Omega)

  4. 大&theta;表示法(Theta Notation(&theta;))：**表示算法确界**。g(x)是f(x)的确界，**界定函数的渐进上界和渐进下界**。对所有n，当n>=n0，如果存在两个常数c1，c2，使得c1g(n)<=f(n)<=c2g(n)，则 f(n)= θ(g(n)) 的时候，代表着g(n)为f(n)的渐进紧确界。

     ![大theta](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/大theta)

  5. 小o表示法(small Oh Notation(o))：与大O的区别为小o表示法的定义中不能取等号

     

     **space and time complexity: use Big Oh Notation**

     一般使用大O表示法，确定上界

+ **例子**

  **选择排序：**

  ```java
  public static void SelectionSort(int [] a, int n){
      //sort the n number in a[0:n-1].
      for(int size=n; size>1; size--){ 
          int j = Max(a,size);
          swap(a[j],a[size-1]);
      }
  }
  ```

  + 分析：

    1. Max(a, size)需要(size - 1)次比较，故总比较数：

       n-1+n-2+……+3+2+1=(n-1)*n/2

    2. 元素移动的次数：

       3(n-1)	*因为swap需要三条语句*

  **插入排序：**

  ```java
  public static void InsertionSort( int [ ]a, int n){
      for(int i=0;i<n;i++){ 
          //insert a[i] into a[0:n-1]
          int t=a[i];
          int j;
          for(j=i-1; j>=0&&t<a[j]; j--)
              a[j+1]=a[j];
          a[j+1]=t;// 此时j是不成立时的j了，而后面的一个元素已经移动到了后后面，所以应该是j+1
      }
  }
  ```

  + 插入排序是指在待排序的元素中，假设前面n-1(其中n>=2)个数已经是排好顺序的，现将第n个数插到前面已经排好的序列中，然后找到合适自己的位置，使得插入第n个数的这个序列也是排好顺序的。按照此法对所有元素进行插入，直到整个序列排为有序的过程，称为插入排序

  + 分析：
    
    1. 最好*（已经排序好了）*：n - 1
    
       移动次数：2(n - 1)*（把a[i]移到t，再从t放回a[i]）*
    
    2. 最坏*（每一次内层循环都要全部遍历）*：（(n-1)n)/2，
    
       移动次数：(1+2)+(2+2)+…..+(n-2+2)+(n-1+2) = n*(n-1)/2+2*(n-1)=(n2+3n-4)/2
    
       *（1+2是指这个数前面的1个数要移动到后一格，这个数字要移出来一次，再放到前面一次，故+2）*

  **利用count来计算执行步数**

  ```java
  public static Comparable Sum( Comparable[] a, int n){ 
      Comparable tsum = 0 ;
      count++;
      for (int i = 0 ; i<n ; i++){ 
          count++;
          tsum += a[i] ;
          count++;
      }
      count++;
      count++; 
      return tsum;
  }
  ```

  + 分析：
    1. 使用全局变量count来计算程序执行的步数。

  **折半查找：**

  ```java
  public static int binarySearch( Comparable [ ] a, Comparable x ){ 
      int low = 0, high = a.length - 1;
      while( low <= high ){ 
          int mid = ( low + high ) / 2;
          if( a[ mid ].compareTo( x ) < 0 )
              low = mid + 1;
          else if( a[ mid ].compareTo( x ) > 0 )
              high = mid – 1;
          else 
              return mid;
      }
      return NOT-FOUND;
  }
  ```

  + 折半查找的前提是数据**已经排好序了**，但排序的时间不算在查找里面，排好了序可以查找很多次。查找中的每次可以排除一半的数据，**需要注意每次用compare比较后，如果不是要找的元素，那么这个mid就被抛弃了**
  + 分析：
    1. 最好：1次
    2. 最坏：log~2~n （log~2~n层）
    3. 平均：O(log~2~n)

  

  **最大连续子序列问题：**

  ```java
  public static int maxSubSum1( int [ ] a )
  { 	int maxSum = 0;
  	for ( int i = 0; i < a.length; i++ )
  		for ( int j = i; j < a.length; j++ )
  		{ int thisSum = 0;
  			for ( int k = i; k <= j; k++ )
  				thisSum += a[k];
  			if ( thisSum > maxSum )
  				maxSum = thisSum;
  		}
  return maxSum;
  }
  ```

  - 穷举所有情况，复杂度O(n^3)

  ```java
  public static int maxSubSum2( int [ ] a )
  { int maxSum = 0;
  	for( int i = 0; i < a.length; i++ )
  	{ int thisSum = 0;
  		for ( int j = i; j < a.length; j++ )
  		{ thisSum += a[j];
  		if ( thisSum > maxSum )
  			maxSum = thisSum;
  		}
  	}
  return maxSum;
  }
  ```

  - 算法1的优化，不需要第三层循环，在第二层循环中，每次加一个元素就与maxSum比较一次

    复杂度O(n^2)

  ```java
  public static int maxSubSum3( int [ ] a ){
      return maxSumRec( a, 0, a.length – 1 );
  }
  
  private static int maxSumRec( int [ ] a, int left, int right ){ 
      if ( left = = right )
          if ( a[ left ] > 0 )
              return a[ left ];
      else return 0;// 如果只有一个元素，那么看这个元素的正负，如果为负，那就返回0，即在不加上时最大，为0，此时的最大子序列为空
      
      int center = ( left + right ) / 2;
      int maxLeftSum = maxSumRec( a, left, center );
      int maxRightSum = maxSumRec( a, center + 1, right );
      int maxLeftBorderSum = 0, leftBorderSum = 0;
      
      for ( int i = center; i >= left; i-- )
      { 
          leftBorderSum += a[i];
          if ( leftBordersum > maxLeftBorderSum )
              maxLeftBorderSum = leftBorderSum;
      } 
      
      int maxRightBorderSum = 0, rightBorderSum = 0;
      
      for ( int i = center + 1; i <= right; i++ ){ 
          rightBorderSum += a[ i ] ;
          if ( rightBorderSum > maxRightBorderSum )
              maxRightBorderSum = rightBorderSum;
      }
    return max3( maxLeftSum, maxRightSun,
                  maxLeftBorderSum + maxRightBorderSum );
  }
  ```

  + 把问题分成两个大小相似的问题，假设已知分解后的问题的答案，如果能推出原问题的答案，那么算法就是成功的

    如上求一串数据的最大子序列

    则可以把数据分成两半，假设已知两半数据的最大子序列（这里运用递归思想来实现），那么对于原数据的最大子序列，只有**三种情况**：等于左边的最大子序列；等于右边的最大子序列；等于一个横跨中间点的序列

    对于第三种情况的求解：**从中间点出发（因为必须横跨中间点）**，分别逐个加上，算中间点左边的最大子序列和中间点右边的最大子序列，**利用一个max记录逐个加入数据的最大值（如下）**，最后把左边的最大值和右边的最大值加起来就可以

  + 分析：
    
    1. 分阶段：把问题分成两个**大致相等**的子问题，然后递归地对它们求解。 
    
    2. 治阶段： 将两个子问题的解合并到一起，可能再做些少 量的附加工作，最后得到整个问题的解。
    
    3. **复杂度：O(n(log n))**
    
       因为递归每层都是O(n)（第一层O(n)，因为两个循环会遍历所有元素，第二层有被分成两个，每个都是O(n/2)，所以每层还是O(n)），而一共是logn层，所以复杂度是乘起来O(nlogn)
    
       ![1](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/divide_and_conquer.png)

   **Euclid’s Algorithm辗转相除法：**

  ```java
  public static long gcd( long m, long n )
  { 	while( n != 0 )
  	{ 
      	long rem = m % n;
  		m = n;
  		n = rem;
  	}
  return m;
  }
  
  ```

  - 分析

    辗转相除，最开始不需要判断m和n的大小，因为当m<n时，第一次循环就会使得m和n进行交换

    要得到辗转相除法的次数最多，如13以内次数最多，那么就要符合这样的数列1 2 3 5 8 13……类似斐波那契数列，**因此要次数最多则m取13，n取8**

    因为斐波那契数列是对数量级，所以这个算法的**复杂度是O(logn)**

- **Keys:** 计算指令行数 * 平均指令执行时间

## 总结
- **各种复杂度：**
  1. Selection Sort —— O(n^2^)
  2. Bubble Sort —— O(n^2^)
  3. Rank Sort —— O(n^2^)
  4. Sequential Search(顺序查找) —— O(n)
  5. Insertion Sort —— O(n^2^)
  6.  Binary Search —— O(log~2~n)
  7. MAXIMUM SUBSEQUNCE SUM PROBLEM —— O(n^3^) or O(n^2^) or O(n(logn))
  8. Euclid’s Algorithm —— O(logn)

- 计算需要执行的指令行数 => 计算大O O(N(n)) 
ex: 执行 N(n) = n^2^ + 5 * n + 1，则复杂度为 O(n^2^ + 5 * n + 1) = O(n^2^)

