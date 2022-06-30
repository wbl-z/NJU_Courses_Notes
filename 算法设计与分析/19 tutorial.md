# 19 tutorial

## 1. is it a forest

![image-20220418111012679](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418111012679.png)

只要一个连通分量没有环，那么就是一棵树

那么只要一个图中没有环，那么就是森林

**判断无向图是否有环，只要DFS判断是否有BE即可**

*无向图中DFS只有TE和BE*

【且如果是树，那么边的数目为**n-1**，如果是森林，那么边的数目为**n-k**(k为树的个数)】

## 2. The Cost of a Graph

![image-20220418112504073](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418112504073.png)

DFS

和关键路径的DFS一模一样，递归找到可达的最小值即可

因为是有向无环图，所以不存在BE

![image-20220418112647270](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418112647270.png)

## 3. :star:Cycle Containing e

![image-20220418113523076](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418113523076.png)

假设边e的两边顶点为a、b

**把e删去**，**从a出发DFS，如果能够到达b**，说明存在另外一条路径可以到达b，**因此有环**，否则当对aDFS结束都没有访问到b，说明无环

## 4. Sorting ill-Behaved Children

![image-20220418114247659](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418114247659.png)

![image-20220418120158858](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418120158858.png)

## 5. :star:A Vertex that reaching all the others

![image-20220418120443108](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418120443108.png)

![image-20220418120449877](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418120449877.png)

将有向图**变成收缩图**后，一定无环，**因此可以将麻烦的有环问题转换成无环问题**

<font color = #ff000>注意在这个问题中，**并不要求原图有入度为0的点**，而是要求收缩图中有入度为0的点，如果这个点在原图中是**若干点构成的环**，如B和E那样，那么B和E都是可以到达其他所有顶点的点，即为符合条件</font>

收缩图是==**有向无环图，** **那么至少有一个点的入度为0**==【*充分条件，反过来不一定成立，如已经有环，再加一个无入度的顶点指向环中任意一个顶点，即有入度为0的顶点，但图不是无环图*】

> proof：假设不存在入度为0的顶点，那么从**任意一个顶点出发，选择它的任意一条入边，按入边方向反方向走**，并将该白色节点变成灰色，下一个顶点同样如此，显然，因为所有顶点都有入度，因此这个过程只会终止于一个灰色节点，从而形成了环，**与无环矛盾**，因此至少存在一个入度为0的顶点
>
> 
>
> ==**因此将所有边反向，有向无环图一定至少有一个出度为0的点**==，反过来同样不一定成立
>
> *another proof：或者沿着任意一条出边走，一定会终止于出度为0的点*



==**如果只有一个入度为0的点，通过入度为0的点，一定可以到达所有点**==

> proof：和上面的proof一样，选择除这个入度为0的点外的任意一个点，选择任意一条入边往回走，因为不存在环，那么最终一定会终止于这个入度为0的顶点。
>
> **对任意一个顶点均是如此**，那么说明从这个入度为0的顶点出发，**存在到达任意一个点的路径**

**如果有多个入度为0的点，那么一定不存在一个点，通过该点可以到达所有点**

> 如果存在多个，那么对于任意两个个入度为0的点，它们都无法相互达到，即不可能

**同理：**

==**如果只有一个出度为0的点，所有点一定都能到达出度为0的这个点**==

**如果有多个出度为0的点，则不存一个点，所有点都可以到达它，因为两个出度为0的点不能相互到达**

## 6. 供水问题

![image-20220418121733899](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418121733899.png)

和题目5一模一样

## 7. 端点问题

![image-20220418131759170](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418131759170.png)

![image-20220418132057231](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418132057231.png)

![image-20220418132417821](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418132417821.png)

:star:bc是需要的，联系前面的问题5，是将图变成收缩图，判断其中的入度为0的点的个数，如果为1，则肯定存在，但这个点是收缩的，即其中可能会包含多个点，因此在这题中，找到了唯一一个出度为0的点，那么说明收缩图中至少有一个出度为0的点，且这个点中在原图只包含一个点，但可能在收缩图中有多个点出度为0，只不过其他的点中包含多个点，所以这种情况是不行的，因此必须要有bc进行判断。

这题另外的解法就是用问题5中的解法，同时找到收缩图中唯一的一个出度为0的点后，再看其中是不是只包含一个点

## 8. Help the mayor

![image-20220418142715522](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418142715522.png)

![image-20220418142723798](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220418142723798.png)

问题1 即任意两个点都是可以到达的，因此即整个图为一个强连通分量，利用强连通分量算法判断即可，时间为线性时间

问题2 即从town hall出发所能到达的点，一定又能从这个点返回，**说明存在环，==那么为了方便分析，转换成收缩图==**，在收缩图中可见，只要sink SCC中的点出发后，才一定能回来，因为sink SCC内部是强连通，而又不会到其他外面的SCC中去。因此只要判断town hall是不是在sink SCC中即可

【*注意在收缩图中，**一旦出去到了其他SCC中，则不可能再回来这个SCC**，否则成环*】

