# Tree 树

![image-20211026093308062](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211026093308062.png)

## 1. Tree 树
- **定义：**节点的集合。**非空的树有唯一的节点root**，**并有许多子树** T1 , T2 , ……, Tk。
- Tree = T(r, Ti)
- r = root 根节点
- 高度 = max{left height, right height}+1
- 子树(各个节点以下为一棵树，兄弟节点之间为`无序的`)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.1.1.png)

### Component 组成
- `Degree of node 节点的度`：**子节点**数目
- `Degree of tree 树的度`：所有子节点中最大的度
- `Leaf 叶节点`：度为0的节点(没有任何子节点)
- `Branch 分支`：度不为0的节点(中间节点)
- `Level 高度(层数)`：根节点的高度为0(也有人说1)，其后所有节点的高度为其父节点加一
- `Depth of tree 树的深度`：树的最大高度

## 2. Binary Tree 二叉树
- 与树的定义相同。
- 所有`节点的度 <= 2，degree可以为1（如果两个subtree中一个为empty）`，`子节点为有序的`，左至右依序称为左子树(left sub tree)和右子树(right sub tree)
- **与树的不同：**
  1. 每个二叉树的元素**只有两个子树**（可以为空子树）。
  2. 二叉树的节点是**有序的**（分成左和右）。

### 性质（高度均从0开始）
1. n 个节点的二叉树，有 n-1 条`边(edge)`（**理解：从root开始，每多一个节点，就会多一条边**）

2. 第 i 层最多有 2^i^个节点(i>=0)

3. 高 h 的二叉树`最少有 h+1 个节点`，`最多有 2^(h+1) -1 个节点`（h>=0）
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.1.png)

4. 叶节点个数n~0~，度为二的节点个数为n~2~，有n~0~ = n~2~ + 1（这里分支数即为边的数目）![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.2.png)

5. n 个节点的二叉树`最大为 n-1 层`，`最小为 [log2(n+1) -1] 层`（由性质3推出）

   > n个节点，高度最多当然n-1（从0开始），最小则把每层尽可能铺满再铺下一层，因此是log~2~(n+1)-1

### Full Binary Tree 满二叉树
- 高 h 的满二叉树有 2^(h+1)^ - 1 个节点 (**完全填满**)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.3.png)

### Complete Binary Tree 完全二叉树

**完全二叉树**的节点是不确定的，任意多个节点都能构成完全二叉树，**铺节点的顺序的从上往下，从左往右**（铺满一层再铺下一层，如果铺不满，从左往右铺）

- 除了最后一层之外，**较低层全部填满**的树
- 高度为 h 的完全二叉树，最少有 **2^h^** 个节点`(最后一层仅一个节点`2^h+1^-1-2^h^+1`)`，最多有 **2^(h+1)^ - 1** 个节点
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.png)
- **性质：**（从0开始编号）
  1. 第 i (0 <= i <= n-1)个插入的节点，i=0 时为树根，i>0 时父节点为 **floor[(i-1)/2]**(`向下舍入`)
  2. 节点i的左子节点为**2i + 1**。如果2i + 1 >= n，节点i没有左子节点，自然也没有右子节点。
  3. 节点i的右子节点为**2i + 2**。如果2i + 2 >= n，节点i没有右子节点。
- 如果从1开始编号

  - 一个节点编号为i的父节点编号是**[i/2]**
  - 一个节点编号为i的左子节点编号**2\*i**
  - 右子节点编号是**2*i+1**
### Binary Tree Representation 二叉树的实现
- **数组**(将树视为完全二叉树，参照序号i作为下标)

  如果不是完全二叉树，那么就把它看作完全二叉树，在没有节点的位置空着就行，相当于补成二叉树

  但对于和完全二叉树**差距较大**时（**高度很高，但节点数很小时**），是**不适合**用完全二叉树的方式来表示，因为需要补很多节点，也就是数组中有很多空缺![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.5.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.6.png)

- **链表**
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.7.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.8.png)

- **向量表（游标表示）** **（静态链表实现）**[（静态链表）](https://www.cnblogs.com/dongry/p/10210609.html)—— 表示的树如上图Example`当0号下标有数据的时候，那么空节点就不能用0表示，所以改成-1，如下图`
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.9.png)

### Operation 操作(方法)
1. BinaryTree create() 创建二叉树
2. boolean isEmpty() 判断树是否为空
3. Node root(x) 取根节点
4. BinaryTree makeTree(root, left, right) 创建二叉树
5. BinaryTree breakTree(root) 清空二叉树
6. ArrayList<T> preorder() 前序遍历
6. ArrayList<T> inorder() 中序遍历
6. ArrayList<T> postorder() 后序遍历
6. ArrayList<T> levelorder() 按层遍历

### Traversal 遍历
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.10.png)![image-20211117194249296](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211117194249296.png)

前三种是左子树在右子树前面，也是主要介绍的三种遍历方法，后三种是右子树在左子树前面（只要把树是左右交换一下即可，因此可以认为是重复的）

#### 递归实现

```c++
Preorder traversal 
template<class T> 
    void PreOrder(BinaryNode<T>* t) // t是树的指针
{// preorder traversal of *t. 
    if(t)// 树不为空
    {
    	visit(t);// 访问，也即输出这个节点
		PreOrder(t->Left);
    	PreOrder(t->Right);
	}
}
```

```c++
Inorder traversal 
template<class T> 
    void InOrder(BinaryNode<T>* t) 
{// inorder traversal of *t. 
    if(t)
    {
		InOrder(t->Left);
        visit(t);
    	InOrder(t->Right);
	}
}
```

```c++
Postorder traversal 
template<class T> 
    void PostOrder(BinaryNode<T>* t) 
{// postorder traversal of *t. 
    if(t)
    {
		PostOrder(t->Left);
    	PostOrder(t->Right);
        visit(t);
	}
}
```

#### 非递归实现（通过栈来模拟递归）

1. Preorder 先序遍历(前序)：VLR

2. Inorder 中序遍历：LVR

   ```c++
   void Inorder(BinaryNode <T>* t){ 
       Stack <BinaryNode<T>*> s(10);
       BinaryNode<T>* p = t;
       for ( ; ; ){ 
           //每次进循环压栈所有左子树，直到左子树为空，那么这时候就该打印父节点了，出栈一个并打印，再将p指向出栈节点的右子树，因为父节点已经打印了，接下来就该打印右子树了
           while(p!=NULL){ 
               s.push(p); 
               p = p->Left; 
           } //将所有左子树压栈，栈底为root
           
           if (!s.IsEmpty( )){ 
               p = s.pop( );
               cout << p->element;
               p = p->Right; //p变右子树
           }else 
               return;
       }
   }
   ```
   
3. Postorder 后序遍历：LRV

   ```c++
   void Postorder(BinaryNode <T> * t){ 
       Stack <StkNode<T>>s(10);
       StkNode<T> Cnode;
       BinaryNode<T> * p = t;
       for( ; ; ){ 
           //tag为0，左子树遍历完了。tag为1，右子树遍历完了。
           while (p!=NULL){ 
               Cnode.ptr = p; 
               Cnode.tag = 0; 
               s.push(Cnode);
               p = p->Left;
           } //将所有左子树压栈，栈底为root
           
           Cnode = s.pop( ); 
           p = Cnode.ptr;
           
           while ( Cnode.tag == 1){ //从右子树回来 
               cout << p->element;
               if ( !s.IsEmpty( )){ 
                   Cnode = s.pop( ); // 因为后序遍历输出父节点后就说明右子树已经遍历了，因此不像LVR，需要把p变成右子树，而是继续pop
                   p = Cnode.ptr; 
               }else 
                   return;
           }
           
           Cnode.tag = 1; 
           s.push(Cnode); 
           p = p->Right; //从左子树回来
       }//for
   } 
   ```

   相比于中序遍历，**后序遍历需要多一个标号，用来确定是左子树遍历完了，还是左右子树都遍历完了**，因为中序遍历左子树遍历完就可以打印出父节点，再遍历右子树，因此栈中存放的就是binaryNode。而后序遍历要遍历左子树，再遍历右子树，再回到根节点，打印出根节点，这里栈中存的是带tag的节点

4. Levelorder 按层遍历：依完全二叉树编号按序遍历
    ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.11.png)

### 建立一颗二叉树

+ 利用MakeTree函数

+ 利用先序、中序唯一的构造一棵二叉树

  **已知前序和中序能唯一的构造一棵二叉树**，**已知后序和中序也能**，但已知先序和后序可能会出现二义性，如只有两个节点，那么到底是树根的右节点为空，还是树根的左节点是空，是不确定的

  ![image-20191228184911507](assets/image-20191228184911507.png)

  > 例子：根据先序的第一个可以确定根节点，再通过中序可以把根节点左边和右边拆成左子树和右子树
  >
  > ![image-20211225224448105](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225224448105.png)![image-20211225224423223](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225224423223.png)
  >
  > 

+ 利用二叉树的广义表表示来构造一棵二叉树

  ![image-20191228184920428](assets/image-20191228184920428.png)

+ 利用二叉树的后缀表示来构造一棵二叉树（当然前缀表达式也可以）

  ![image-20191228184926076](assets/image-20191228184926076.png)
  
  > 例子：![image-20211225224752401](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225224752401.png)
  >
  > ```java
  > public void createTreeByPostorder(String expr) {
  > 		Stack stack = new Stack();
  > 		for (int i = 0; i < expr.length(); i++) {
  > 			char c = expr.charAt(i);
  > 			if (IsOperand(c)) 
  >             {// 遇到操作数,压栈
  > 				BinaryNode node = new BinaryNode(c, null, null);
  > 				stack.push(node);
  > 			 } 
  >                 else {//遇到操作符
  > 				BinaryNode rt = null, lt = null;
  > 				if (IsDoubleOperator) 
  >                 {    //二元操作符
  > 					if (!stack.empty()) 	
  >                     {
  > 						rt = (BinaryNode) stack.pop();
  >                     }
  > 			            if(!stack.empty()) 	 
  >                         {
  > 							lt = (BinaryNode) stack.pop();
  >                         } 
  > 				}	   
  > 				else 
  >                 {                     // 一元操作符 
  > 					if (!stack.empty()) 
  >                     {
  > 						rt = (BinaryNode) stack.pop();
  >                     }
  >                     lt=null;
  > 				}
  > 				//创建一颗新树，并压入堆栈
  > 				BinaryNode node = new BinaryNode(c, lt, rt);
  > 				stack.push(node);
  > 			}
  > 		}
  > 		if (!stack.empty()) {//将root引用指向新树的根节点
  > 			this.root = (BinaryNode) stack.pop();}}
  > ```

### Binary-Tree Representation of a Tree 树的表示法

+ 广义表表示：a(b(f,g),c,d(h,i,j),e)

+ 双亲表示法（即节点的中有指向父节点的索引，如f的父节点是2号节点b）

  ![image-20191228190655238](assets/image-20191228190655238.png)

+ 左子女—右兄弟表示法（**从而把任意的树转化为二叉树**）

  ![image-20191228190651111](assets/image-20191228190651111.png)

### Forest -> Binary Tree 森林 转 二叉树

- Forest 森林：**多棵树的集合**
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.12.png)

1. 将每棵树转为二叉树（利用左子女-右兄弟表示法）
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.13.png)

2. 将所有子树的根节点以右链（兄弟）相连
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.14.png)

### 一般的树遍历

+ **深度优先遍历：**
  
  1. 先序次序遍历（**先根**）与对应的左子女—右兄弟的二叉树的**先序**遍历一致
  
  2. 后序次序遍历（**后根**）与对应的左子女—右兄弟的二叉树的<font color=#ff00>**中序**</font>遍历一致
  
  3. 注意到我们并没有定义一般树的中根遍历，因为**子结点该怎么分两部分并没有定义**，所以**只定义先、后根**。
  
     ![image-20211225202534254](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225202534254.png)![image-20191228191603569](assets/image-20191228191603569.png)
  
+ **广度优先遍历：**

  1. 分层访问

     ![image-20211117202420494](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211117202420494.png)

### 森林遍历

+ **先根次序遍历：** 
  
  1. 访问F的第一棵树的根 
  2. 按先根遍历第一棵树的子树森林 
  3. 按先根遍历其它树组成的森林
  4. 等于**左子女-右兄弟表示的二叉树的先序**
+  **中根次序遍历（先中根遍历第一个子树，访问根，再中根遍历剩下的子树）：** 
  
  1. 中序遍历第一棵树的根结点的**所有子树**；
  2. 访问森林中第一棵树的根结点；
  3. 中序遍历去掉第一棵树后的子森林。
  4. 等于**左子女-右兄弟表示二叉树的中序**
+ **后根次序遍历：** 
  1. 按后根遍历第一棵树的子树森林 
  
  2. 按后根遍历其它树组成的森林 
  
  3. 访问F的第一棵树的根
  
  4. 等于**左子女-右兄弟表示二叉树的后序**
  
     ![image-20191228191515186](assets/image-20191228191515186.png)![image-20211117203155913](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211117203155913.png)

+ **广度优先遍历（层次遍历）**

  <img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211117203451068.png" alt="image-20211117203451068" style="zoom:150%;" />

  注意这里是对原来的森林，如果是左子女-右兄弟的二叉树，那么应该是斜着来



## 3. String 字符串

### Component 组成
1. string 串：字符组成的有限序列(用""包起来)
2. length 串的长度：字符个数，不包括分界符("")和结束字符('\0')
3. null 空串：不包含任何字符的串(或只包含结束字符的串)
4. subString 子字符串：串中任意连续子序列

### Operation 操作
1. String create() 创建字符串
2. int length() 求串长
3. String concat(string1, string2) 连接两个字符串(并置)
4. String subString(start, end) 取子字符串
5. int find(subString) 求子串第一次出现的位置
6. (Java) boolean equals(Object obj) 比较字符串是否相等
6. (Java) char charAt(int index) 字符在串中第一次出现的位置

## 4. Thread Tree 线索树
+ **目标：**n个结点的**二叉树**有2n个链域（`有2n个指针`）， 其中真正有用的是n – 1个（即`n-1条边`），其它n + 1个都是空域。**为了充分利用结点中的空域，使得对某些运算更快。**

- 增加前驱(上一个被输出的节点)与后继(下一个被输出的节点)的指针，加速遍历运算
- 根据**多加的标识位**(leftThread、rightThread)**判断子节点**(leftchild、rightchild)**存的是什么**
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.4.1.png)
- <img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225211603575.png" alt="image-20211225211603575" style="zoom:67%;" />
- **不同遍历顺序对应不同的线索方式**（下面以中序为例子）

![image-20191228192711619](assets/image-20191228192711619.png)

- 中序遍历线索树（**既不需要递归，也不需要用栈**）![image-20211225212341938](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225212341938.png)

1. 找到第一个节点：根节点的最左下节点为第一个节点first![image-20211225211431986](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225211431986.png)

2. 寻找后继：

   - 如果这个节点没有右子树，即rightthread==1，那么右孩子就指向后继

   - 如果这个节点有右子树，即rightthread==0，那么**右孩子的最左下节点就为后继**

     ![image-20211225211509766](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225211509766.png)

     上面补充return current;

     ![image-20211117210302133](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211117210302133.png)![image-20211117210333215](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211117210333215.png)

     **构建中序搜索树**

     在中序遍历的**基础上**，不输出节点，并且判断pre（pre不等于null）的有没有右孩子，如果没有就把rightthread设为1，并把rightchild设为p，同理判断p有没有左孩子，如果没有就把leftthread设为1，并把leftchild设为pre

     ![image-20211117210526889](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211117210526889.png)![image-20211117210501545](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211117210501545.png)

     ![image-20211225212811549](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225212811549.png)

## 5. Huffman Tree 霍夫曼树
- **增长树：**将原树度为 0 的节点添加 2 个外节点，度为 1 的节点添加 1 个外节点
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.5.1.png)
- **霍夫曼树：**给定n个权值作为n个叶子结点，构造一棵二叉树，若带权路径长度达到最小，称这样的二叉树为最优二叉树，也称为霍夫曼树(Huffman Tree)。

### Properties 属性
1.  外通路长度（外路径）E：根节点到**外节点**(度为 0，也就是后来添加的节点)的路径长总和   
    ex: 3 + 3 + 2 + 3 + 4 + 4 + 3 + 3 = 25
2.  内通路长度（内路径）I：根节点到**内节点**(度不为 0，也就是原本的节点)的路径长总和    
    ex: 2 + 1 + 3 + 2 + 1 + 2 = 11
3.  带权路径长：路径乘以节点的权重

### Representation 表示
- m 个数作为外节点构造霍夫曼树（增长树中的一种）

  ![image-20211225222706273](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225222706273.png)

- ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.5.2.png)

- 平衡时即上图第三种情况，**外通路长度是最小的（但霍夫曼树不一定）**，因为此时把一个节点如11的长度少1，那么11占据父节点，因此如3的节点变成一个节点，3和2变成这个节点的子节点，那么结果就是一个节点长度-1，而会有两个节点长度+1，因此总长度变大

### Huffman算法

+ **思想：** 权大的外结点靠近根， 权小的远离根。 
+ **算法：** 
  1. 假设有W1、W2、、、、Wm个权值。
  2. 从这些权值中找出两个最小值W1，W2构成新的权值W=W1+W2,也就是建立一棵二叉树，这个二叉树表通过该结点的频度。
  3. 然后对剩下的权值W， W3，W4，…Wm 经由小到大排序，
  4. 重复2、3直到剩一个权值，也就是树的根。
+ 当内结点的权值与外结点的权值相等的情况下， 内结点应排在外结点之后。即在**第二步中构造出的二叉树W如果和给定序列中的相同，应该放在给定序列相同值的后面**

### Huffman Code 霍夫曼编码

- 将各个字符的使用频率作为权值，构造霍夫曼树
- 左子树标号 0，右子树标号 1，路径编码作为字符的霍夫曼编码。**为了译码，任一字符的编码不应是另一字符的编码的前缀**
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.5.3.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.5.4.png)
- 这样就可以用短的编码表示使用次数多的字母，用长的编码表示使用次数短的字母，是一种**变长编码**，相比于所有字母用统一长度编码，**可以使得总长度更短**

## 6. General List 广义表
- 序列中元素可以是另一个序列

### Properties 属性
1. 长度：元素个数
2. 深度：所含元素最大层数
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.6.1.png)

### Operation 操作
1. Node head(list) 取表头
2. Node tail(list) 取表尾
3. Node first(list) 取第一个元素
4. T info(node) 取元素内容
5. Node next(node) 下一个元素
6. Class<T> nodeType(node) 返回元素类型(原子或是子表)
7. boolean push(list, element) 插入元素
8. boolean addon(list, x)
9. boolean setinfo(element, x) 设置节点内容
10. boolean sethead(list, x) 设置表头
11. boolean setnext(element1, element2) 设置下一个元素
12. boolean settail(list1, list2) 设置表尾

- Node 类型
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.6.2.png)

# Specific Trees

## 1. Binary Search Tree 二叉搜索树

### Definition 定义

二叉搜索树可以为空树，如果它不是空树，那么它具有如下性质

### Properties 属性

1. 任两个节点的键(key)不相等

2. 节点左子树的键**都比**节点的键小

3. 节点右子树的键**都比**节点的键大于或等于

4. 左/右子树分别也是一棵二叉搜索树
    ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.1.1.png)

  ### index Binary Search Tree 标号二叉搜索数

  1. 由二叉树衍生，增加Leftsize。
  2. Leftsize的值 = **左子树的元素个数 + 1**

![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.1.2.png)![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.1.3.png)

+ **查找**：（复杂度：**树的高度**）

  ```java
  private BinaryNode find( Comparable x, BinaryNode t ) 
  { 
      if( t = = null ) // 对空值的判断
          return null;
  	if( x. compareTo( t.element ) < 0 ) 		
          return find( x, t.left );
  	else if( x.compareTo( t.element ) > 0 ) 
          return find( x, t.right );
  	else 
          return t; //Match
  }
  ```

+ **插入：**（复杂度：树高）

  ```java
  private BinaryNode insert( Comparable x, BinaryNode t ){ 
      if( t = = null )
          t = new BinaryNode( x, null, null );
      else if( x.compareTo( t.element ) < 0 )
          t.left = insert( x, t.left );
      else if( x.compareTo( t.element ) > 0 )
          t.right = insert( x, t.right );
      else
          ; //找到了就不用插入了duplicate; do nothing
      return t;
  }
  ```

+ **删除：**（复杂度：树的高度）（只会向下，不会返回向上）

  1. 对于叶节点，直接删除
  2. 对于只有一个子树的节点，删除后让子树的root替代原来节点即可
  3. 对于有两个子树的节点：
     1. 删除节点
     2. 找**左子树最大的节点或右子树最小的节点**来代替删除的节点位置。
     3. 删除替代的节点原来位置上重复的节点。（**递归**，**把删除这个节点的问题转换成删除用来替换的节点的问题。删除这个节点同样分叶节点，只有一个子树的两种情况**，*但不会出现第三种情况*，因为如果是左子树最大节点，那这个最大节点一定没有右子树，否则它不是最大节点）
  
  ```java
  private BinaryNode remove( Comparable x, BinaryNode t ){ 
      if( t == null )
          return t;
      
      //找要删除的值x
      if( x.compareTo( t.element ) < 0 ) //过大
          t.left = remove( x, t.left );
      else if( x.compareTo( t.element ) > 0 ) //过小
          t.right = remove( x, t.right );
      else if( t.left != null && t.right != null ){ // 要删除的就是t
          t.element = findMin( t.right ).element;
          t.right = remove( t.element , t.right );// 把删除这个节点的问题转换成删除用来替换的节点的问题
      }else
          t = ( t.left != null ) ? t.left : t.right;// 包含了一个子树和无子树的情况，无子树那就是null，所以t=null
      return t;
  }
  ```
  

因此上述算法的**最好情况是树的高度最小，复杂度最好为O(log~2~n)**

## 2. AVL Tree 平衡树
- **Purpose 目的：**提高二叉搜索树的效率并减少平均搜索长度（通过**减少树的高度**来实现）

- **高度：**平均高度 —— O(log~2~n) = **搜索的时间复杂度（对数复杂度）**

  ![image-20211225232157511](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225232157511.png)

- **定义：**

  1. **二叉搜索树**。
  2. 每个节点满足|左子树高度 - 右子树高度| $\le$ 1。

- **平衡因子**（可选，如果有可以使得一些算法速度更快）

  ![image-20211119175543913](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211119175543913.png)

- **平衡方法：**从不平衡的那个节点开始往下看，分为4种类型

  1. 右侧外外 —— 左单旋（提右降左）= 左下旋

  ![image-20191228200950068](assets/image-20191228200950068.png)![image-20211225232736078](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225232736078.png)

  2. 右侧外内 —— 先右后左

  ![image-20191228201344007](assets/image-20191228201344007.png)

  3. 左侧外外 —— 右单旋（提左降右）= 右下旋

  ![image-20191228201552714](assets/image-20191228201552714.png)

  4. 左侧外内 —— 先左后右

  ![image-20191228201626577](assets/image-20191228201626577.png)
  
- 调整只要在包含插入结点的**最小不平衡子树**A中进行,即从根到达插入结点的路径上,**离插入结点最近的**。**<font color =#ff00>调整不会影响到以A为根的子树以外的结点，只会影响到A及其子树</font>**

  从**不平衡节点往下看<font color=#ff00>两层</font>**，如果是左左/右右，那么就是外侧，只需要单旋转**（把不平衡节点的下一层旋转到这一层）**；如果是左右/右左，那么需要双旋转**（把不平衡节点的下下层旋转到下层，再旋转到这一层）**

  ![image-20211123082110062](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211123082110062.png)

### Properties 属性
1. 符合二叉搜索树的要求
2. 左子树高度和右子树高度相差 <= 1
3. height 高度：最深节点的层数作为树的高度
4. Balance Factor 平衡因子：**右子树高度减左子树高度**
5. height 高度：n 个节点的AVL树高度为O(log~2~n)

### Special Operation 特殊操作
- insert 插入：插入后可能引发高度不平衡 -> 旋转 —— 最坏：O(log~2~n)

  ![image-20211123085645704](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211123085645704.png)

  1. 单旋转(LL, RR 外侧)：由 A(h+3){B(h+2){BL(h+1), BR(h)}, C(h)} -> B(h+2){BL(h+1), A(h+1){BR(h), C(h)}}
     ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.2.1.png)
  2. 双旋转(LR, RL 内侧)：执行两次单旋转
     ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.2.2.png)
  3. EX: 依序列{A, Z, C, W, D, X ,Y} 构造AVL
     ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.2.3.png)
     ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.2.4.png)

- deletion 删除

  这里中序后继即右子树的最小节点，当然也可以选择左子树的最大节点（即中序前继）

  ![image-20211123092406331](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211123092406331.png)

  ![image-20211225235330154](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225235330154.png)![image-20211225235336355](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211225235336355.png)

### 代码

1. AVL Tree![image-20211123084725404](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211123084725404.png)
2. 插入![image-20211123084916280](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211123084916280.png)![image-20211123084929467](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211123084929467.png)
3. 左单旋和左双旋![image-20211123085003068](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211123085003068.png)

## 3. m-way Tree m路搜索树

计算机更多使用m路搜索树，原因是cache的块加载机制（总是加载一个块），这样一次就可以把一个节点载入，在节点内顺序查找下一个节点，而m路搜索树的高度低于二叉搜索树，所以时间花费可能更低

### Prperties 属性
1. 所有节点至多有 **m 个子节点**(度最大为 m)，由 p = m-1 个标记(element)分开
2. 有 p 个标记的节点，必有恰好 p+1 个子节点
3. height 高度：n 个元素的树的高度最小为 **log~m~(n+1)** 层，最多为 n 层（从1开始）
4. nodes 节点数：高度为 h 的树最少有 h (一层一个)个节点，最多有 **m^h^ - 1** 个元素（从1开始）（所以7等比求和后，分母如6用一个节点最多6个元素乘后被消去了）

![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.3.1.png)
```
key(C0) < k1 < key(C1) < k2 < ... < kp < Cp
ki <= Ci <= k(i+1)
```
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.3.2.png)



## 4. B Tree B树(Balenced-Tree)
- 二叉搜索树 -> (带平衡条件) -> 平衡二叉搜索树(AVL 树)
- m路搜索树 -> (带平衡条件) -> 平衡m叉搜索树(B-树)

### Definition (Properties) 定义(属性)
1. m阶的B树是一个m路搜索树。

2. 根节点**至少有两个**子节点

3. **除了根节点之外所有内节点至少有 ceil(m/2) 个子节点（向上取整），同理至少要有floor(m/2)个标记**

    ![image-20211126163159579](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211126163159579.png)

4. 每个节点的标记数目不能超过(m -1)。

5. 所有外节点都在**同一层** 
    ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.1.png)

6. 外节点数 = 元素的个数（标记的个数） + 1
    ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.2.png)

B树有时会放在外存中，如果很大的数据量，会放在磁盘上，有的还会放在网络上，所以**B树是可能不在内存中的**，考试时也会涉及。如果不在内存中，通常一次载入一个节点，这样可以把m的值设的大一点，这样一次载入就可以加载很多个标记。所以节点内的查找不是主要矛盾，对磁盘很慢的读取速度才是主要矛盾![image-20211126164537619](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211126164537619.png)所以要尽可能把树的高度降低，减少对磁盘的访问次数

高为h的B树：**log~m~(n+1)<=h<=1+log~m/2~ (n+1)/2**

### Operation 操作
1. **search 搜索：**任何搜索不超过 h(高度) 次 —— O(h)
2. **insert 插入：**插入发生在外节点上面一层(必为内节点)  
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.3.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.4.png)![image-20211126171910542](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211126171910542.png)

- 若插入了含有m-1 个关键码(key)的节点(full node)，因为节点已经满了，所以需作分裂：取**中间元素**（**ceil（m/2）**）为上一层的关键码，**如果树根发生了分裂，那么树的高度将要加1**![image-20211126172125388](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211126172125388.png)
- EX 1
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.5.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.6.png)
- EX 2
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.7.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.8.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.9.png)

3. deletion 删除：分成三种情况
    1) 用后继点取代删除键值
    2) （要删除的节点不在叶子节点，above level）![image-20211126173753112](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211126173753112.png)
    3) 若为叶子节点。
       - 若该节点含有 >= ceil(m/2) + 1 个节点：直接删除
       - 若该节点含有 >= ceil(m/2) 个节点：删除后会不满足B
         - 若兄弟节点节点含有 >= ceil(m/2) + 1 个节点：向旁边最靠近借一个(**父键下移，兄弟节点键上移**)![image-20211226101959047](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226101959047.png)
         - 若兄弟节点都只含有 == ceil(m/2)个节点：父键下移，并与兄弟节点组成一个节点。如果根节点被合并了，那么高度减1<img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211126172952026.png" alt="image-20211126172952026"  /><img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211126172723537.png" alt="image-20211126172723537"  />

![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.10.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.11.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/4.2.4.12.png)