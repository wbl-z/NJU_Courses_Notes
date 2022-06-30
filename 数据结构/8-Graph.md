# Graph 图

## Definition 定义
- G = G(V, E)：V 顶点(`vertex`)集合、E 边(`edge`)的集合
- Undirected Graph 无向图：边为双向(或称为无向)，即 (v0, v1) = (v1, v0)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.1.png)
- Directed Graph 有向图：边为有向(可能单向可能双向 <start, end>)， 即 <v1, v2> != <v2, v1>
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.2.png)
- 不讨论多重边({**<v1, v2>, <v1, v2>,** ...})或自反边({<v1, v1>})（如果是方向相反的两个有向边，不是多重边）
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.3.png)

## Properties 属性(性质)

### Degree of Vertex 顶点的度
- **TD(v) 度**：以 v 为端点的边的数量
- **ID(v) in-degree 入度**：进入 v 的边的数量
- **OD(v) out-degree 出度**：离开 v 的边的数量
- TD(v) = ID(v) + OD(v)
- 图中所有**边的数量** e = $\Sigma$(TD(vi))/2 = 所有点的度的总和/2（因为每一条边被算在了两个顶点的度中）

### SubGraph 子图
- 对于 G = G(V, E)，G' = G'(V', E')，其中 V' 为 V 的子集，E' 为 E 的子集，**且E' 的所有端点都在 V' 内**，称 G' 为 G 的子图
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.6.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.7.png)

### Path 路径
- p: i1, i2, i3, ..., ik：由i1到i2到...ik的边的有序集合，**路径上的每一个节点都不能重复，只能是唯一的**

#### Simple Path 简单路径
- 起点与终点不同

#### Cycle Path 回路
- 起点与终点相同

### Connected 连通的
- 若存在一条路径 p 从 vi 到 vj(p = vi, ..., vj)，称vi, vj为连通的
- **对无向图**来说，如果**任意的两个顶点**连通，则此图是连通的

## Category 分类

### Undirected Graph 无向图
- 图中**每个节点至多有 n-1 个边**，**n 个节点**的图共有 r 个边，有 $r\le\frac{n(n-1)}{2}$

### Complete Graph 完全图(完全无向图)
- 若边数$r=\frac{n(n-1)}{2}$，即每个节点有 n-1 个边，称为**完全无向图**
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.4.png)

### Directed Graph 有向图
- 图中每个节点至多有  $2(n-1)$ 个边(**进入&离开**)，n 个节点的图共有 r 个边，有  $r\le n(n-1)$

### Complete Directed Graph 完全有向图
- 若边数 $r= n(n-1)$，即每个节点有 n-1 个离开的边与 n-1 个进入的边，称为**完全有向图**
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.5.png)

#### Connected Graph 连通图和连通组件
- 若**无向图**中所有点都是连通的

- 若图不是连通的，各子连通图称为`Branch 分支`，非连通图有极大连通子图（在图中取子图外的任意一个顶点，和子图均不连通，就是极大的），极大连通子图也称为**连通组件**

- `Maximum connected subgraph 极大子连通子图`又称为`Connected Component 连通组件`

  ![image-20211210172650596](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210172650596.png)

#### Strong Connected Graph 强连通图和强连通组件
- 对**有向图**中每个顶点对(i, j)都存在 **i 到 j 和 j 到 i** 的路径
- 同理非强连通图也有**强连通组件**

### Network 网路
- 当赋予**边权重**(weight / cost)时，称为（无向/有向）**加权图(**Weighted Graph/weighted digraph)。
- 网络指**加权**的**连通**图。
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.8.png)

### Spanning tree 生成树

+ 一个**<font color=#ff00>连通图</font>的生成树**是他的`minimum connected subgraph 极小连通子图`。(在连通图中不断去边，在保证连通的前提下，直到不能再去边为止)
+ 一个**有n个节点的生成树有(n - 1)个边**。

![image-20191229100407661](assets/image-20191229100407661.png)

## Representation 表示

### Adjacency 邻接的
- 某个边 e 的两端点为 v1, v2，则称 v1, v2 为邻接的

#### Adjacency Matrix 邻接矩阵

+ G=(V,E), V={V1 ,V2 ,……,Vn }

+ A(i,j)= 1 if <i,j>,<j,i>属于E or (i,j)属于E ，A(i,j) = 0 otherwise

  ![image-20211210174244523](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210174244523.png)

+ **无向图的矩阵是对称的。**所以无向图只需要矩阵的一半即可得到完整信息，而有向图则需要整个矩阵才能得到完整的信息

+ 无向图一行/一列**所有元素的和**就是这个行/列对应顶点的**度**![image-20211210174556775](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210174556775.png)

+ 有向图的**行所有元素的和是顶点的出度，列是对应入度**![image-20211210174728747](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210174728747.png)

+ 对于网络network，邻接矩阵中记录的是权重（**把1换成权重，把0换成∞**，表示不连通，当然无穷不能表示，可以用一个记号来表示即可）

  **A(i,j)表示的是i->j**![image-20211210175054236](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210175054236.png)
  
  ![image-20211210175146525](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211210175146525.png)

![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.10.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.11.png)

#### Linked-Adjacency List 邻接链表
- 使用线性表(元素序号为数组下标)，带上链表(链表中是所有与这个顶点邻接的顶点，**一般从序号小到大链接**)，多少个顶点就多少个单链表

- 当**顶点多但边数少**时，减少储存需求。（如果用邻接矩阵，那么一定需要n*n的空间）

- 无向图中所有链表的**节点数的和**是**边的数量的两倍**（因为一条边会被用两次）

- 有向图中所有链表的**节点数的和**等于**边的数量**。可以使用邻接表，也可以是逆邻接表

  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.12.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.13.png)

#### Adjacency Multilist 多重邻接表
- 邻接链表对于同一条边会存在多个节点，使用多重邻接表可减少节点数量(一条边一个节点)

  在无向图中, 如果边数为m, 则在邻接表表示中需2m个单位来存储. 为了 克服这一缺点, 采用邻接多重表, 每条边用一个结点表示.

- 无向图
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.14.png)

- 有向图（一定要起点写在前面，终点写在后面）
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.15.png)

## Operation 操作

### Traversal 遍历
- 自树/图中某个顶点出发访问所有顶点，并且**每个顶点只访问一次**。
- **遍历二叉树：**前序, 中序, 后序
- **遍历树：** 
  1. 深度优先遍历 (先根,后根) 
  2. 广度优先遍历 
- **遍历森林：** 
  1. 深度优先遍历 (先根,中根,后根) 
  2. 广度优先遍历 
- **遍历图：**
  1. 深度优先遍历 DFS (Depth First Search) 
  2. 广度优先遍历 BFS (Breadth First Search)

#### DFS Depth First Search 深度优先算法
- 访问顶点 v0，然后访问其中一个未被访问的**子节点**，递归访问
- 若不存在未被访问的子节点，**退回到路径上含有未被访问子顶点的顶点**，访问该顶点未被访问的子节点，**<font color=#ff00>递归实现</font>**。
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.16.png)

```c++
//主过程
template<NameType,DistType> void Graph<NameType,DistType> :: DFS( )
{
int *visited=new int[NumVertices];
    for ( int i=0; i<NumVertices; i++)
        visited[i]=0; 
    DFS(0,visited); 
    delete[] visited;
}
//子过程
template<NameType,DistType> void Graph<NameType,DistType> :: 
DFS(int v,visited[]){ 
    cout<<GetValue(v)<<'';
    visited[v]=1;
    int w=GetFirstNeighbor(v);
    
    while (w!=-1){ 
        if(!visited[w]) 
            DFS(w,visited);
        w=GetNextNeighbor(v,w);// 找到v中w后的下一个邻接顶点
    }
template<NameType,DistType> int Graph<NameType, DistType> :: GetFirstNeighbor(int v) // 是在邻接矩阵中找到，找到的第一个有边连接的点，col表示column柱，如果是邻接表同理
{ 
    if (v!=-1) 
	{ 
        for( int col=0; col<CurrentVertices; col++) 
            if (Edge[v][col]>0 && Edge[v][col]<max) 
                return col;
	} 	
    	return -1;
}
```

- **算法复杂度：**邻接表 O(n + e)，邻接矩阵 O(n^2^)，**其中e指的是边的条数（邻接表中没有连接起来的顶点不用访问，而邻接矩阵需要遍历全部）**

#### BFS Breadth First Search 广度优先遍历
- 访问顶点 v0，先访问 v0 的所有子顶点 v1, v2, ..., vk，然后依序访问 vi(i=1~k)中没有被访问过的子顶点，**<font color=#ff00>非递归实现</font>**。
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.17.png)

```c++
template<NameType,DistType> void Graph<NameType,DistType> :: BFS(int v){
    int* visited=new int[NumVertices];
    for (int i=0; i<NumVertices; i++) 
        visited[i]=0;
    cout<<GetValue(v)<<'';
    visited[v]=1;
    queue<int> q;// 广度优先遍历均通过队列实现
    q.EnQueue(v);
    
    while(!q.IsEmpty()){ 
        v=q.DeQueue();
        int w=GetFirstNeighbor(v);
        while (w!=-1){ 
            if(!visited[w]){ 
                cout<<GetValue(w)<<'';
                visited[w]=1;
                q.EnQueue(w);
            }
            w=GetNextNeighbor(v,w);
        }
    }
    delete[] visited;
}
```

- 每个顶点进队列一次且只进一次，算法中循环语句至多执行n次。
- **算法复杂度：**邻接表 O(n + e)，邻接矩阵 O(n^2^)

#### 连通分量：对于非连通无向图

但当无向图(以无向图为例)为非连通图时，从图的某一顶点出发进行遍历(深度，广度)**只能访问到该顶点所在的最大连通子图**(即连通分量)的所有顶点.

+ 连通分量 = 最大连通子图

- 对**每个分支做一次遍历即可**
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.18.png)

- 即**遍历每一个顶点**，如果它没有被访问过，那么就进行DFS

  ![image-20211217164708392](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211217164708392.png)

### Spanning Tree 生成树
- 生成树：**含有 n 个顶点与 n-1 条边的子图**![image-20211217165035980](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211217165035980.png)

  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.9.png)![image-20211217165458765](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211217165458765.png)

  **生成树不唯一**

  

#### Minimum-cost Spanning Tree 最小(代价)生成树
- 找到个**边权值总和最小**的生成树
- 一棵树的`极小连通子图(Mimimum Connected Graph)`称为最小生成树
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.9.1.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.9.2.png)
### 贪心算法（逐步求解（Grandy)的策略）（每次只根据当前情况选择最优的）

- **Kruskal 算法 克鲁斯卡尔：**G(V, E)，取 E' = {} —— *添加最小边到图里*
1. 每次找出 E 中最小权值的边 ei(**同时不使 E' 中的边形成回路**)

2. 使 E = E - {ei}, E' = union(E', {ei})

3. 递归直到 |E'| = n-1，即存在 n-1 个边，恰好将 n 个顶点连通在一起

   ![image-20211217170032332](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211217170050921.png)![image-20211217170101397](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211217170101397.png)

4. 算法分析：

   **建立e条边的最小堆**：

   + e 边的条数、n 顶点个数
   + 检测邻接矩阵O(n^2^ )
   + 每插入一条边，执行一次最小堆入堆 -> fiterup() 算法：log~2~ e -> 总的建堆时间为O(elog~2~ e) —— 最坏情况（采用的是第二种堆的建立方法）

   **构造最小生成树**：

   + e次出堆操作：每一次出堆，执行一次filterdown(), 总时间为O(elog~2~ e)
   + 2e次find操作：O(elog~2~ n) —— 并查集查找（**对一条边的两个顶点查找它们的并查集**，如果相同，说明它们已经连通，所以会形成回路，这条边要丢弃）
   + n-1次union操作：O(n) —— 并查集合并（接上，如果并查集不相同，那么就加入这条边，把并查集合并，事实上其中一个顶点的并查集只有它自己，因为最开始是删除了所有边的）
   + 总的计算时间为 O(elog~2~ e + elog~2~ n + n^2^ + n)

```c++
void Graph<string , float>::Kruskal(MinSpanTree&T){ 
    MSTEdgeNode e;
    MinHeap<MSTEdgeNode>H(currentEdges);//H为 最小生成树边的最小堆
    int NumVertices=VerticesList.Last , u , v ;
    Ufsets F(NumVertices); //建立n个单元素的连通分量，即并查集
    
    //建立边的类并加到最小堆里面
    for(u=0;u<NumVertices;u++)
        for (v=u+1;v<NumVertices;v++)// 注意是u+1，因为这里是对于无向图，不能重复地加入边
            if(Edge[u][v]!=MAXINT){ 
                e.tail=u;
                e.head=v;
                e.cost=Edge[u][v];
                H.insert(e);
            }
    
    int count=1; //生成树边计数
    while(count<NumVertices){ 
        H.RemoveMin(e);
        u=F.Find(e.tail); 
        v=F.Find(e.head);
        
        if(u!=v){// 通过并查集find是否连通
            F.union(u,v);
            T.Insert(e);
            count++;
        }
    }
}
```

- **Prim 算法 普里姆 O(n^2^)：**G(V, E) —— *每到一个顶点找最小边出去*
1. 取 V 中**任意一个顶点**，使 N = {v0}, E' = {}

2. 找到与 N 中任意顶点相连的边权重最小的边 e0，将 e0 的另一端点 vi(vi 不在 N 中)，使 N = union(N, vi), E' = union(E', e0)

3. 递归直到 |N| = n, |E'| = n-1，即选中 n 个顶点与 n-1 条边，构成最小生成树

4. 算法分析：下面的计算得到的是n^3^，但可以通过**使用邻接矩阵来改进效率**，使得复杂度降低到n^2^

   ![image-20211217173356622](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211217173356622.png)

  + 时间复杂度：n + n(n + n) = O(n^2^ )

![image-20211217172729577](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211217172729577.png)![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.9.3.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.9.4.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.0.9.5.png)

![image-20211226200449690](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226200449690.png)![image-20211226200407103](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226200407103.png)

```c++
void graph<string,float>::Prim(MinSpanTree&T){ 
    int NumVertices=VerticesList.last;
    float*lowcost=new float[NumVertices];
    int * nearvex=new int[NumVertices];
    for (int i=1;i< NumVertices;i++){
        lowcost[i]=Edge[0][i]; // 这里把0作为第一个顶点加入生成树
        nearvex[i]=0;
    }
    nearvex[0]=-1;
    MSTEdgeNode e;
    for (int i=1; i< NumVertices; i++){ 
        float min=MAXINT; int v=0;
        for ( int j=1; j< NumVertices; j++)
            if(nearvex[j]!=-1&&lowcost[j]<min){
                v=j; 
                min=lowcost[j];
            } //for j, 选择最小的边
        if (v){ 
            e.tail=nearvex[v];
            e.head=v;
            e.cost=lowcost[v];
            T.Insert(e);// 加入最小生成树
            nearvex[v]=-1;// 把nearvex的改成-1
            for(int j=1; j< NumVertices; j++)// 看生成树外的顶点到刚加入的顶点的距离是不是比原来的短，如果是，修改距离，并在nearvex种改成这个新加入的顶点
                if( nearvex[j]!=-1 && Edge[v][j]<lowcost[j] ){ 
                    lowcost[j]=Edge[v][j]; 
                    nearvex[j]=v;
                }
        } //if
    } //for i
}
```

### Shortest Path 最短路径

- v 到 w 的所有路径中，权值(cost 代价)总和最小的路径
- ![image-20211221080304554](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211221080304554.png)

#### Dijkstra 算法(非负权值单源最短路径)（迪科斯彻）
- 图中所有边的权值非负(**>=0**)

- 计算图中**某点 v0 到其他各点 vi 的最短路径**

- 原理：不可能从一条长路径绕到一个顶点比短路径的长度短

  **选定一个顶点v~0~，找到v~0~到其他顶点的直接路径长度，其中对于最短的那条，就是v~0~到对应的顶点v~i~的最短路径，因为从v~0~到其他点的路径都比这条路径长，不可能通过从其他的路径绕到其他点v~j~再到v~i~比这条最短的路径更短**。这样就确定了到一个顶点v~i~的最短路径

  接下来就以刚刚已经确定了最短路径的顶点v~i~作为中转站，看v~0~通过这个点到其他点的距离会不会更短，如果比之前一步的更短，那么就更新。否则就不变。在除了v~0~,v~i~之外的其他顶点的路径都根据v~i~作为中转站更新/不更新后，其中的最短路径就是v~0~到对应的顶点v~k~的最短路径。原理和上面第一次的一样：即不可能通过除了v~0~,v~i~之外的其他顶点（路径更长），绕出比此时的短路径更短的路径

  ![image-20211221083222900](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211221083222900.png)

  用**两个数组**分别记录

  - **当前最短路径**
  - **这个最短路径的路线是怎么样的** *（记录v~0~到这个顶点的前一个顶点，这样一次次往回找就能找出路径，如最后4的前1个顶点为2，2的前一个顶点为3，3的前一个顶点为0，因此路径为0-3-2-4）*

- 步骤
1. 选择起始点 v0，使 S = {v0}，E = {}，E' 为 p:s, vi(s 为 S 中的点)，即 S 中元素到非 S 中元素的最短边的集合
2. 选择权值(代价)最小的边 ei 加入 E，即 E = union(E, {ei})，S = union(S, {vi})
3. E 中的元素必表示 v0 到 s 的最短距离(s 为 S 中元素)
4. 更新 E' 集合，重复2,3步骤直到所有点的最短距离都找到
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.3.1.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.3.2.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.3.3.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.3.4.png)

```c++
void Graph::shortestpath(int n,int v){ 
    for( int i=0; i<n; i++){ //初始将除v外所有点初始为v直连的边长
        dist[i]=Edge[v][i];
        s[i]=0;              //s[i]==1表示点i已加入，后续遍历时就不用看已经加入的顶点，通过!s[i]作为条件
        if( i!=v && dist[i]< MAXNUM ) // 如果与v连通，那么路径设为v，否则为-1
            path[i]=v;
        else 
            path[i]=-1;
    }
    
    s[v]=1; 
    dist[v]=0;
    for( i=0; i<n-1; i++){ //共遍历n-1次
        float min=MAXNUM; 
        int u=v;
        for( int j=0; j<n; j++)//选择未加入的最近的点加入
            if( !s[j] && dist[j]<min ) { 
                u=j; min=dist[j];
            }
        s[u]=1;
        for ( int w=0; w<n; w++)//计算经过新点到其他点的距离
            if( !s[w] && Edge[u][w] < MAXNUM &&
               dist[u]+Edge[u][w] < dist[w]){
                
                dist[w]=dist[u]+Edge[u][w]; 
                path[w]=u;
            }
    }//for
}
```

- **复杂度：**O(n^2^)

#### Bellman-Ford 算法(任意权值(可为负)单源最短路径)(贝尔曼-福特)
- **任意权值是允许权值为负数，但不允许出现<font color=#ff00>回路权值和为负数</font>的情况**，这样可以一直在这条回路上走，最终出现负无穷的值，就没有意义了
- 原理为**动态规划**（**<font color=#ff00>要根据上一步的所有情况来确定下一步的最优</font>**），因为权值可以为负，所以dijkstra算法（贪心算法）不适用（权值为正的情况才行，从原理上可以理解）
- 构造最短路径长度数组，**dist^i^[u]为从源点(起点)经过 i 条边到达 u 的最短路径长度**
- 带负权值边不可构成回路(v0 [+a]-> v1 [-b] -> v0，相当于不动而长度自减)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.3.5.png)

```c++
void Graph::BellmanFord(int n, int v){ 
    for(int i=0;i<n;i++){ 
        dist[i]=Edge[v][i];
        if(i!=v&&dist[i]<MAXNUM)
            path[i]=v;
        else 
            path[i]=-1;
    }
    
    for (int k=2;k<n;k++)// n-2次迭代，路径最长为n-1，第一次迭代在上面的循环z已经进行了
        for(int u=0;u<n;u++)
            if(u!=v)
                for(i=0;i<n;i++)
                    if (Edge[i][u]!=0 && Edge[i][u]<MAXNUM && dist[u]>dist[i]+Edge[i][u])						{
                            dist[u]=dist[i]+Edge[i][u];
                            path[u]=i;
                        }
}
```

- 复杂度：最好为 O(E)，最坏 O(VE)，平均O(VE)

#### Floyed 算法 所有顶点的最短路径(非负权值环【即不能存在权值和为负数的环】)

Floyd算法又称为**插点法**，是在路径中逐个插入点，看是否会变短的一种方法

- 计算**所有顶点的最短路径**的两种方式
  1. 执行 Dijkstra 算法 n 次
  2. Floyed 算法（**算法形式更简单**）

- 复杂度：都是 O(n^3^)

- Floyed 算法步骤
1. 以邻接矩阵表示，初始矩阵为 A0，自反边长度为 0，未连通视为无限
    ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.4.1.png)

2. **作 n-1 次迭代(路径最多长 n-1)**，每次令 **A~k~[i, j] = min(A~k-1~[i, j], A~k-1~[i, k] + A~k-1~[k, j])**，即上次迭代最短路径(<v~i~, v~j~>)与再经过一条边(<v~i~, v~k~, v~j~>)的路径（即要**<v~i~,v~k~>+<v~k~,v~j~>**，即邻接矩阵中的**A~k-1~[i, k] + A~k-1~[k, j]**）取最小值作为新的最短路径(<v~i~, v~j~>)

3. 所有对于每一个元素，**横向找到第k列的元素+纵向找到第k行的元素即可**，如下

  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.4.2.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.4.3.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.4.4.png)

```c++
void Graph::Alllength(int n){ 
    for(int i=0; i<n; i++)// 两层循环初始化A和path矩阵
        for(int j=0; j<n; j++){ 
            a[i][j]=Edge[i][j];
            if(i==j) a[i][j]=0;
            if(i!=j&&a[i][j]<MAXNUM)
                path=i;// 最开始就是<i,j>边，因此i->j的前一个顶点就是i
            else 
                path[i][j]=0;// 当自反时（自己到自己）设为0
        }
    // floyd 算法
    for(int k=0; k<n; k++)
        for(int i=0; i<n; i++)
            for(int j=0; j<n; j++)
                if( a[i][k]+a[k][j]<a[i][j] ){ 
                    a[i][j]=a[i][k]+a[k][j];
                    path[i][j]=path[k][j];// 把i->j路径上j的前一个顶点设为k->j路径上的j的前一个顶点，因为此时是i->...->k->j了。同理要找路径时和Dijkstra一样，一个个往回找，path[i][j]存放这个路径上j的前一个顶点，再去这前一个顶点中找到再前一个顶点
                }
    
}
```

### Activity Network 活动网络

**图的应用**

- 用`顶点`表示活动的网络 AOV 网络
- 用`边`表示活动的网络 AOE 网络

#### AOV Active on Vertex Network 顶点活动网络

**用顶点表示活动，用弧表示活动间的优先关系的有向图称为AOV网。**

- 用顶点表示活动，边表示`先后顺序(符号 -<)`(`偏序关系`（**即没有环**）一个`偏序集`，使用`无环有向图`实现)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.5.1.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.5.2.png)
- 图中顶点表示课程（活动），有向边（弧）表示 先决条件。
  若课程i是课程j的预修课程，则图中有弧<i,j>
- 图中存在边 <i, j>，称 i 为 j 的`直接前驱`，j 为 i 的`直接后继`
- 图中存在路径 p:i -> j，称 i 为 j 的`前驱`，j 为 i 的`后继`

#### Topological Sort 拓扑排序
- 图 G(V, E) 中 V 的线性排序

  ![image-20211221094521551](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211221094521551.png)

- **条件：**若存在边 <i, j>，则线性序列中 i 必须在 j 前面

- **算法步骤：**通过**无环有向图**进行拓扑排序
1. 寻找图中入度为 0 的节点 ei(存在多个则**次序任意**)（注意并不是一次删除所有度为0的顶点，再去找度为0的顶点，而是一次删一个，然后再在所有里面找度为0的顶点）

2. **删除 e~i~ 与所有 e~i~ 的出边**

3. 递归直到所有节点都被消去，删除顺序即为拓扑排序

   ![image-20211221094659861](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211221094659861.png)

- **Implement 实现**

  ![image-20211221094807598](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211221094807598.png)

  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.5.3.png)
  ![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.5.4.png)

  ```c++
  void Graph :: Topologicalsort ( )
  { 1. int top=-1; 
    2. for ( int i=0; i<n ;i++ ) 
        	if (count[i]= =0) {count[i]=top ; top =i;}//相当于压栈过程，count[i]中存放top，而top指向的是当前度为0的节点，因此conun[i]指向这个节点，然后又使得top=i，就是把i压入栈中
    3. for (int i=0 ; i<n ; i++) 
        	if (top= =-1){cout <<―Network has a cycle‖<< endl; return;} 
   		else { 
              1) int j=top; top=count[top]; // j=top相当于出栈，把栈顶的元素弹出，top=count[top]就是使得top指向下一个度为0的节点，这是在2.中完成的
              2) cout<<j<<endl; 
              3)Edge<float> *l = NodeTable[j].adj; 
              4) while(l) 
              	{ 
                  int k = l.dest;
                  if ( --connt[k] = = 0){ count[k] = top; top = k; }// 压栈
                  l = l->link;
              	}
          	}
   }
  ```

- **算法分析：**
  
  1. n个顶点，e条边 
  2. 建立链式栈O（n） 
  3. 每个结点输出一次，每条边被检查一次O（n＋e） 
  4. 复杂度：O(n+n+e)

#### AOE Active on Edge Network 边活动网络(事件顶点网络)
- 边代表活动，顶点代表事件(状态)，**边上权重代表活动需要时间**
- 存在**唯一入度为 0 的点**(源)，为起始状态
- 存在**唯一出度为 0 的点**(汇)，为终止状态
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.5.5.png)

##### Critical Path 关键路径
- 从开始到结束**最长的路径**(时间瓶颈)*（代表了项目所需的最短时间，上面的所有活动都是要完成的，最短的时间就是一刻不停地完成时间线最长的任务，如果两个活动中间有间隔，那么就会更长）*

  （如上面的18，**注意不同活动是可以同时进行的，a~1~和a~2~和a~3~是可以同时进行的**）

- 相关变量
1. Ve[i] 最早发生时间：为 v0 -> vi 的**最长路径长度**（因为要把前面所有事先工作做完才能做vi，因此找前面路径最大值）

2. Vl[i] 最迟发生时间：为 **Ve[n-1] - (Vi -> Vn-1 的最长路径)**（下一个动作 j 至少要Ve[j]个时间，因此我这个事件可以在Ve[j] - <vi, vj>的时间前完成就行）**（如果是关键路径上的顶点，那么最早和最迟都是一样的）**

   （是在保证汇点Vn-1 在Ve[n-1]时刻(18)完成的前提下， 事件Vi允许发生的最晚时间＝Ve[n-1]－Vi ->Vn－1的最长路径长度。即只要能不拖进度即可）

   ![image-20211224163556482](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211224163556482.png)

3. e[k] 表示活动 ak= <vi, vj>的最早开始时间，**e[k] = Ve[i]**

4. l[k] 表示活动 ak=<vi, vj>的最迟开始时间，**l[k] = Vl[j] - dur(<i,j>)**

5. `Slack time` 松弛时间：l[k] - e[k] 事件`最早可能开始时间`与`最迟可能开始时间`的差

6. l[k] == e[k]  —— ak是**没有时间余量**的**关键活动（不能推迟或提前）**

   ![image-20211226211151392](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226211151392.png)


- 寻找关键路径算法步骤：
1. 定 Ve[0] = 0，推出所有 Ve[i] 的值，也就是其S余点的最早可能发生时间![image-20211224164553692](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211224164553692.png)![image-20211226211503477](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211226211503477.png)
2. 由 Ve[n-1] 逆推，推出所有 Vl[i] 的值，也就是其余点的最迟可能发生时间![image-20211224164605171](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211224164605171.png)
3. 1,2步骤都必须依照**拓扑排序顺序**，且 Ve[i] 必须算出所有前驱才能计算，Vl[i] 必须算出所有后继才能计算![image-20211224164628552](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211224164628552.png)

##### Implement 实现(Representation 表示)
- 使用**邻接表表示**，且下标顺序已为一个拓扑排序
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.5.6.png)
![Error](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/8.5.7.png)
```c++
void Graph ::CriticalPath ( ){ 
    int i , j ; 
    int p, k ; float e, l ;
    float * Ve=new float[n]; 
    float * Vl=new float[n];
    
    for (i=0; i<n ; i++) //求Ve，初始化所有Ve=0
        Ve[i]=0;
    for (i=0; i<n ; i++){ //取每一个点，将其后续点根据边权关系赋值Ve
        Edge <float> * p=NodeTable[i].adj;
        while (p!=NULL){ 
            k = p. dest;//修改开始时间小于当前时间加上边权的后续点
            if (Ve[i]+p. cost > Ve[k]) // 如果相加比当前的大，取大的
                Ve[k]=Ve[i]+p.cost ;
            p=p.link;;//获取当前点的下一个后续点
        }
    }//求Vl，将所有点初始化为结束点开始时间，因此需要先求出Ve
    for (i=0; i<n ; i++)Vl[i]=Ve[n-1];
    for (i=n-2; i>=0 ; i--){ //取每一个点，将其时间根据后续权赋值
        p=NodeTable[i].adj;
        while(p!=NULL){ 
            k=p. dest;//如果当前点开始时间大于后续时间减去边权
            if (Vl[k]-p.cost<Vl[i])
                Vl[i]=Vl[k]-p. cost ;//则修改
            p=p. link;//获取下一个后继点
        }
    }
    for (i=0; i<n ;i++){ 
        p=NodeTable[i].adj;
        while (p!=NULL){ //最早开始时间==最迟的点为关键点
            k= p. dest;
            e=Ve[i]; 
            l=Vl[k]-p. cost ;// 要减去才知道到底是从i到哪里为关键路径，如果是求出关键的事件，那么直接比较Ve和Vl即可。这里后面减去dur之后相等说明就是
            if(l= =e)
                cout<< "<" <<i<< "," << k 
                << " > "<< "is critical Activity" << endl;
                p=p. link;
        }
    }
}
```

- **复杂度**
1. 拓扑排序求 Ve[i] + 逆拓扑排序求 Vl[i] O(n + e)
2. 求各活动 e[k], l[i] O(e)
3. 全部 O(n + e)

