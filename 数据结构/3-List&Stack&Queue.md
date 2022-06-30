# List, Stack and Queue

## ADT

+ **定义：**一群对象及对象操作的集合。
+ **数据对象：**一些值(value)以及实例(instances)的集合。例如：Boolean、NaturalNumber、String......<img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225111626879.png" alt="image-20211225111626879" style="zoom:50%;" />

## 1. List 列表（线性表） ADT

> **栈和队列**都是特殊的线性表。它们在功能上受到了更多的限制，以适应于特殊用途。

- **有序元素**集合：L = (e0, e1, e2, e3, ..., en)
- e0 is the first element 
- en is the last element 
- ei precedes ei+1

### Operations 操作
1. List create() 创建列表
2. boolean isEmpty() 判断列表是否为空
3. int length() 计算列表长度
4. T find(int k) **查找第k个元素**
5. boolean search(T item) **查找给定元素**
6. boolean delete(int k) 删除第k个的元素
7. boolean insert(T item, int k) 在**第k位后面**插入元素
8. void print() 打印列表

### Impletation 实现1：Array 数组 [ei]
- **定义：**使用数组表示对象的实例。[e1, e2, ..., en]

- **位置查找：**location(i)=i-1 —— O(1)

- **元素查询：**Search(x) —— O(length)

- **删除：**remove(k,x) 删除第k个元素，将它赋值x并返回 —— O(n)

  > 因为删除第一个要把n-1个数据左移，删除最后一个，把0个数据左移

- **插入：**insert (x , i) 插入x在第i个元素后 —— O( n)

  > 同上，但注意插入有n+1种插入方法，删除仅n种情况，如果链表从1开始编号，那么insert(0, h)就是在最开始插入元素

- **问题：**

  1. 查找快
  2. 插入/删除慢

- **应用：**

  1. 多项式ADT —— 问题：指数大时不好储存

     对于指数跨度大的多项式，如果只记录系数，用数组表示，那么会存在很多的零，造成浪费，这种表示称为**稠密表示**
     
     ![3.1.8](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.1.8.png)

### Impletation 实现2：Single Linked List 单向链表 (next, data)
- **定义：**每一个数据对象的节点都有一个link或pointer指向与他有关的另一个节点。0(1, e1), 1(2, e2), ... , n(null, en)

  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.1.1.png)

- 链(chain)是指**一个节点表示一个元素**的链表。

- **最后一个节点**的pointer是**null**。

- **first指向第一个节点**

- **类定义：**

  1. ListNode 代表结点的类 

     > <img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211012082343996.png" alt="image-20211012082343996" style="zoom:50%;" />

  2. LinkedList 代表表本身的类

  3. LinkedListItr 代表位置的类 

     > <img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211012082356976.png" alt="image-20211012082356976" style="zoom:50%;" />

  4. 都是包DataStructures 的一部分

- **查找：**find (object x) —— **O(N)**

- **删除：**Remove( x ) ——  O(1)`但事实上，找到要删除节点的前一个节点findPrevious是O(n)的`

  > ![image-20211008175012942](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211008175012942.png)**first.link就是取出first内的内存地址中的link区的值取出来**，而这个值就是指向下一个节点的内存地址，把它赋值给first，那么第一个元素就变成了第二个，也即删除了第一个元素

  > 要删除指定位置的元素，那么
  >
  > 第一步要找到指向这个元素的元素(before)，也即这个元素的前一个元素
  >
  > ![image-20211008175829255](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211008175829255.png)
  >
  > 第二步要让这个before指向要删除元素的下一个元素，这里就是before.link=before.link.link（即before的下下个元素的地址）

- **查前一个：**Findprevious ( x ) —— O(N)

- **插入：**Insert(x, p) —— O(1)

- **带表头节点的单链表**（注意Dummy Head的存在，而且这还一般在题目中是**默认**的。）

  > ![image-20211012081343570](file://https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211012081343570.png?lastModify=1640402927)
  >
  > 另外一种带表头节点的单链表，具有表头节点dummy node，**不存放数据，而是放一个标识，用来区别出header**
  >
  > 第二个节点才放第一个数据
  >
  > 这样的好处是**不需要对第一个数据做单独处理**，类似在序列前面补零
  >
  > 如果是空表，但**仍然是有表头节点**

- **应用：**

  1. 多项式ADT：记录系数和指数，用单链表表示，省略了中间多余的0，称为**稀疏表示**

     > 逻辑结构：多项式
     >
     > 实现逻辑结构的物理结构（即数据的存储方式（不等同于硬件））：数组或单链表，数组是连续顺序存储，而单链表的链式结构则是把数据存放在任意的存储单元中

     ![3.1.9](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.1.9.png)

     ![image-20211015165936933](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211015165936933.png)![image-20211015173257780](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211015173257780.png)
  
  2. 基数排序 Radix Sort
  
     ![image-20191228155555721](assets/image-20191228155555721.png)
  
     ![image-20191228155605003](assets/image-20191228155605003.png)
  
     > 10进制就设置10个桶，先根据每个数的个位的数字放到对应的桶中，如21放在第一个桶
     >
     > 然后从左往右把桶中数字拿出，**注意是先进桶的先出**，如371先出，531后出，相当于把每个桶中的元素**接连串起来**（这里的桶实际上是一个FIFO的队列）
     >
     > 然后再按十位来进桶出桶，接着是百位，**一直到所有数字中的最高位为止**，此时出桶后的数据就是已经排好序的了
     >
     > 补充：
     >
     > - 基数排序：根据键值的每位数字来分配桶；
     >   - $O(d(n + radix))$d是次数(也即数字的最高位数)，n是元素数量，radix是桶个数
     > - 计数排序：每个桶只存储单一键值；
     >   - 待排序列：9 3 5 4 9 1 2 7 8 1 3 6 5 3 4 0 10 9 7 9
     >     先遍历这个无序的数列，让每一个整数按照值对号入座，对应数组下标的元素加1。
     >     统计结果如下图所示：
     >     数组值：|1 2 1 3 2 2 1 2 1 4 1|
     >     下标值：|0 1 2 3 4 5 6 7 8 9 10|
     >     直接便利数组，输出数组元素的下标值，元素的值是几就输出多少次。
     >     输出结果为：
     >     0 1 1 2 3 3 3 4 4 5 5 6 7 7 8 9 9 9 10
     >   - 计数排序时只以序列的最大值来作为统计数组的长度是不对的，比如排序95 94 96…，这个时候我们可以用数列最大值和最小值得差值加1（max-min+1）作为统计数组的长度。
     >   - **既然计数排序的时间复杂度是 O(N) 那我们为啥不都使用计数排序呢？答案是只有当数字取值规模确定并且比较小的时候才能用呀，如果不知道取值规模或者取值规模太大，就不可以申请出那么多桶了**
     > - 桶排序：每个桶存储一定范围的数值；
     >   - 桶排序是计数排序的扩展版本。桶排序需要尽量保证元素分散均匀，否则当所有数据集中在同一个桶中时，桶排序失效（直接变成了把一个桶中的元素排序，那么桶的过程就没有用了）。
     >   - ![img](https://img-blog.csdnimg.cn/20190219081232815.png)
     > - ![image-20211225161551625](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225161551625.png)

### Impletation 实现3：Double Linked List 双向链表 (prev, next, data)
- **一般：**0(null, 1, e1), 1(0, 2, e2), 2(1, 3, e3), ..., n(n-1, null, en)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.1.2.png)

- **循环：**0(n, 1, e1), 1(0, 2, e2), 2(1, 3, e3), ..., n(n-1, 0, en)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.1.3.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.1.4.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.1.5.png)

### Impletation 实现4：Circular Linked List 循环链表 (next, data)
- 0(1, e1), 1(2, e2), ... , n(0, en)

  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.1.6.png)

  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.1.7.png)

- **应用：**

  1. 约瑟夫问题：

  ```java
  w = m;
  
  for( int i = 1; i<= n-1; i++){ 
      for (int j =1; j<=w-1; j++) rear = rear.link;
      if (i = = 1){ 
          head = rear.link ; p = head; 
      }else{ 
          p.link = rear.link; p = rear.link; 
      }
      rear.link = p.link;
  }
  
  P.link = rear;
  rear.link = null;
  ```

### Impletation 实现5：Cursor implementation of Linked Lists静态链表（游标实现）

+ **用处：**用**游标(即数组下标)**来表示指针实现链表。

  用数组实现链表，不过next中存放的是数组的下标，称为**静态链表**

+ **核心思想：**

  1. 数据储存在一组结构体中。每一个结构体包含有数据及指向下一个结构体的指针。
  2. **一个新的结构体可以通过调用malloc而从系统的全局内存得到**，并可通过调用free而被释放。
3. 分为`数据链表`与`备用链表`。

4. `备用链表`表示游标当前空闲节点的位置。

   ![image-20191228155109176](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20191228155109176.png)![image-20211225142856831](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225142856831.png)
   
   左边是单链表的代码操作（p和next都是指针）
   
   右边是是静态链表的代码操作（要先找到这个下标的节点，p是下标，next也是下标）
   
5. <img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211022165756026.png" alt="image-20211022165756026" style="zoom:50%;" />

   > **系统内存是个单链表**
   >
   > alloc先检查还有没有空余内存，如果没有就OutOfMemory，如果有就把这个单链表中的节点分出去给用户程序，事实上，可以分配出去任何一个空余节点，这里在实现上固定是header后的第一个节点（header不能用来分配）
   >
   > free则是把p指向的节点清空，并**放回到系统单链表的第一个节点**
   >
   > 这样的内存管理是一种最简单的管理

## 2. Stack 栈

- **定义：** **LIFO(last in first out)** 后进先出的线性列表

- 进栈和出栈端称为栈顶(top)，底部称为栈底(bottom)

- **方法**：只有push，pop，peek（查看栈顶元素，不作任何修改）

  因此**栈的操作的复杂度都是O(1)**

  *在一些库中会有延申操作，如isEmpty，事实上都是用唯一的3个操作来组合出来的*

- **实现：**

  1. **链表** topOfStack -> 栈顶（用**listNode**实现）。

     when topOfStack= = **null** is empty stack。

     <img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211022175033402.png" alt="image-20211022175033402" style="zoom:67%;" /><img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211022174957375.png" alt="image-20211022174957375" style="zoom:67%;" />

  2. 数组 

     1） topOfStack -> 栈顶（用**数组下标**表示，因此一个栈会有一个默认大小的属性）。

     ​	   when topOfStack= = **-1** is empty stack。

     <img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211022175042154.png" alt="image-20211022175042154" style="zoom:67%;" />

     2） 当多个栈并存时，很浪费空间（一个数组中的高处不能得到利用）。

     3） 因此**一个数组中放两个栈**可以节省空间（前提是不会在之后相冲突）![image-20191228160838658](assets/image-20191228160838658.png)

  <img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/3.2.1.png" alt="Error" style="zoom: 80%;" />

- **应用：**

  1. 平衡符号（括号匹配） Balancing Symbols(Parenthesis Matching) —— O(n)

      需要遍历所有符号，所以复杂度O(n)

      > 当遇到左括号，把位置压栈，遇到右括号，栈中元素出栈，构成匹配。如果栈中没有元素，不匹配，如果全部遍历完栈中还有元素，不匹配
     
     ![image-20191228161151895](assets/image-20191228161151895.png)
     
     ```c++
     #include <iostream.h>
     #include <string.h>
     #include <stdio.h>
     #include “stack.h”
     const int Maxlength = 100; // max expression length
     void PrintMatchedPairs(char *expr){ 
         Stack<int> s(Maxlength);
         int j, length = strlen(expr);
         
         for ( int i = l; i <= length; i++){ 
             if ( expr[i-1]=='(' )
                 s.Add(i);
             else if (expr[i-1]= =")")
                 try {
                     s.Delete(j); 
                     cout <<j<<' '<<i<< endl;
                 }catch (OutOfBounds){
                     cout << "No match for right parenthesis"
                         << " at "<< i << endl;
                 }
         }
         while ( !s.IsEmpty ()){ 
             s.Delete(j);
             cout<< "No match for left parenthesis at "<< j << endl;
         }
     } 
     
     void static main(void){ 
         char expr[MaxLength];
         cout<< "type an expression of length at most"<<MaxLength<<endl;
         cin.getline(expr, MaxLength);
         cout<<"the pairs of matching parentheses in "<<endl;
         puts(expr);
         cout<<"are"<<endl;
         printMatcnedPairs(expr);
     }
     ```
     
2.  表达式计算 Expression Evaluation
  
   + **后缀表达式计算**（注意后缀表达式是**不需要括号**的）
   1) 开辟一个运算分量栈 
     
   2) 遇分量进栈; 
     
   3) 遇运算符: 取栈顶两个分量进行运算,栈中退了两个分量,并将结果进栈。
   
   + **中缀转后缀**
   
     A+B\*C#---------> ABC\*+#
   
     1) 遇运算分量(操作数)直接输出 
   
     2) 遇运算符：比较当前运算符与栈顶运算符的优先级. 若当前运算符的优先级<=栈顶运算符的优先级, 则把栈顶运算符输出，继续比较下一个运算符; 否则进栈. *因此一开始栈中要放一个优先级最低的运算符, 假设为“#”*（不必要）， 例子： A+B+C； A\*B-C (A+B)\*(C-D)#-------> AB+CD-\*# 
   
     3) 遇‘（’ : 一定压栈，每个运算符都比（优先级高，因此栈顶为（运算符一定压栈. 
   
     4) 遇‘）’ : 不断退栈输出，直到遇到’(’ ，把左括号弹出就结束，即左右括号被消除了
   
     5) 遇‘#’ 或表达式已经遍历完了: 将栈中的所有运算符出栈打印，过程终止。

## 3. Queue 队列(伫列)
- **FIFO(first in first out)** 先进先出

- 进队(enqueue)端称为**尾部(rear)**，出队(dequeue)端称为**头部(front)**

- java具体方法：（左边一列会抛出异常，右边一列不会抛出异常，会返回false/null）（**examine是看头部的元素**）

  ![image-20211026082737291](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026082737291.png)

- **实现：**

  1. 数组

     ![image-20211026082258959](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026082258959.png)

     ![image-20211026082308336](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026082308336.png)![image-20211026082345218](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026082345218.png)

     如果采用front=front+1的方法，虽然复杂度降低到1，但会造成**数组前面有很大的空间没有被使用**，因此采用下面的把数组看成一个环的方法

  2. 环形数组

     - When front or back reachs theArray.length-1, **reset 0** 

     - **back = (back+1) % theArray.length** 

     - **front = (front + 1) % theArray.length**

     - 每次进队，back = back + 1。

       ![image-20211026082421591](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026082421591.png)

       通过**取模的方式**来实现循环

       **进队出队都是常数复杂度O(1)**

  3. 链表

     ![image-20211026083200224](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026083200224.png)

     ![image-20211026083829324](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026083829324.png)

     > ~是析构函数，析构函数（destructor）是成员函数的一种，它的名字与类名相同，但前面要加`~`，没有参数和返回值。
     >
     > 如果不自己写析构函数，那么编译器生成默认析构函数（删除对象中的内容），delete时只会删除这个对象中的两个指针front，back，因为编译器和系统**只看到**它有两个指针，所以只把这两个指针删掉，**而指针指向的对象是不会被删除的**。
     >
     > 因此只删除了queue中的两个指针，而Node节点则不会被删除
     >
     > =>如下就定义了queue的析构函数，从而可把所有节点都删除，就能确保对象运行中用 new 运算符分配的空间在对象消亡时一起被释放
     >
     > ![image-20211026084144380](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026084144380.png)

- **应用**：

  打印出二项式展开的系数

  ![image-20211026090804204](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026090804204.png)

  ```c++
  #include <stdio.h> 
  #include <iostream.h>
  #include “queue.h” 
  void YANGHUI(int n) 
  {
       Queue<int> q; 
       q.makeEmpty( ); 
       q.Enqueue(1);
       q.Enqueue(1); 
       int s=0;
       for (int i=1; i<=n;i++)
       {
           cout << endl; 
           for (int k=1;k<=10-i;k++) 
               cout<<“ ”;
           q.Enqueue(0); // 因为s是代表最左边的元素，上次出栈的元素，s取0，即在最左边补零。这里再enqueue一个0，即在最右边补零。这样就可以表示下面的元素是上面两个元素相加了
           for (int j=1;j<=i+2;j++) 
           { 
               int t=q.Dequeue( ); 
               q.Enqueue(s+t);// 把上面的两个元素相加压入栈中
               s=t; // 把当前出栈的元素作为最左边元素
               if (j!=i+2) 
                   cout<< s <<“ ”;
           }
        }
  }
  ```

  

