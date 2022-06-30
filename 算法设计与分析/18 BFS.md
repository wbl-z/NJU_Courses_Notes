# 18 BFS

并非DFS优于BFS，而是两者的适用面不同

![image-20220417105016009](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417105016009.png)

![image-20220417105245470](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417105245470.png)

显然BFS中**不存在前向边DE/FE**，因为不会从子树返回到父节点

## skeleton

![image-20220417105651492](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417105651492.png)

![image-20220417105916483](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417105916483.png)

增加了**parent**来表明节点的父节点；增加了d来表明**distance**，子节点的d是父节点+1，源节点的d=0

![image-20220417110311998](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417110311998.png)

## Property

### property1

![image-20220417110724875](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417110724875.png)

![image-20220417110912735](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417110912735.png)

**case1：u不可达**，那么因为存在边uv，如果是无向图，那么v肯定不可达。如果是有向图，那么v无论可达还是不可达，都≤∞，因此成立

**case2：u可达**，那么v一定可达，存在uv(u→v)，由于δ是最短路径，所以长度一定≤从s到u后，再从u到v，因此成立

### property2

![image-20220417111437230](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417111437230.png)

进队列时才对节点的d赋值

![image-20220417112412282](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417112412282.png)

证明任意节点成立时：①反证法②数学归纳法

事实上即利用lemma1，递归地证明成立，假设一个节点的父节点u成立d[u]≥δ(s,u)，那么因为是子节点v，所以存在uv，所以δ(v)≤δ(u)+1≤d[u]+1=d[v]，即证明成立

### property3

![image-20220417113428803](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417113428803.png)

![image-20220417114251812](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417114251812.png)

![image-20220417114258750](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417114258750.png)

即根据入队和出队两个**操作进行归纳假设**，讨论两个操作是否会对性质产生影响

### property4

![image-20220417114418690](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417114418690.png)

**d[v]=δ(s,v)成立**，而不是前面弱的性质≥。即由TE构成的d[v]是最短路径δ(s,v)的其中一条（**最短路径可能会有多条，BFS树边构成的仅是其中的一条**）

![image-20220417115858615](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417115858615.png)

![image-20220417115910929](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417115910929.png)

因为是从s到v的最短路径，那么可以断定也是s到u的最短路径。如果不是，那么可以将这条s到u的路径用更短的替换，那么s到v也变得更短了，说明原来的s到v不是最短路径

同时由于我们选取的v是不满足定理1 d[v]=δ(s,v)的所有点中离s最近的点，因此u就一定是满足定理1的，否则u就应该是不满足定理且离s最近的点了

![image-20220417115921110](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417115921110.png)

![image-20220417115958634](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417115958634.png)

## BFS in Directed Graph

![image-20220417120326648](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417120326648.png)

没有前向边

![image-20220417120908244](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417120908244.png)

对于CE【**只可能在同层/上一层指向下一层(此时取=)/下层指向上面若干(1..n)层之间出现**】，是在u出队，访问u的子节点时才会发现CE，并且v一定不是白色，如果是白色，那么v是u的子节点，d[v]=d[u]+1，并且不是CE了，而是TE

**v如果是黑色**，那么说明很早就已经出队列了，d[v]≤d[u]

**v如果是灰色**，那么说明还是队列中，由于此时u出队列，那么v在u的后面，根据property3 在u出队前，u是队首，所以肯定有d[v]≤d[u]+1

## BFS in Undirected Graph

![image-20220417141506926](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417141506926.png)

**没有前向边，也没有后向边**，它们都变成了TE

![image-20220417141921659](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417141921659.png)

对于CE【**只可能在同一层/上一层指向下一层出现，因此只有=和=+1两种情况**，*对比上面的有向图，因为无向，所以有向图的第三种可能:下层指向上面若干层是不会出现的*】，uv，当u出队时，v一定不是白色

**v也不是黑色**，如果是黑色，那么早就出队了，说明它含有的边都已经被访问过了，那么为什么没有访问现在的CE呢

**v一定是灰色**，说明**v还在队列中**，根据property3，那么d[v]=d[u]或者d[v]=d[u]+1

## Ex1:Bipartite Graph 二部图

![image-20220417142633512](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417142633512.png)

二部图：将图中的顶点分成2部分U、V，图的每一条边的两个顶点都分别位于U和V中

![image-20220417142801389](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417142801389.png)

通过染色来判断，将源染成红色，然后BFS，将它的所有未访问的邻居都染成相反颜色，如果在访问中发现某个已经被访问过了，即灰色，那么判断邻居的颜色和节点的颜色是否相反，如果相反，继续，否则说明不是二部图

## Ex2:K-Degree Subgraph K度子图

![image-20220417143212135](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417143212135.png)

![image-20220417143407422](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417143407422.png)

先遍历一遍节点，找到度数小于k的节点入队，因为它们小于k，所以是我们想要去掉的，队列此时表示的是要去掉的顶点

然后按BFS一样，出队，**逐个删除这些顶点的边，删除一条边后，立即判断另一个顶点的度数，如果它小于k并且不在队列中，说明也要被删除，因此将其入队**

## Ex3:搜索问题

### Knight Moves

![image-20220417143848753](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417143848753.png)

![image-20220417144045000](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417144045000.png)

棋盘共有64个格子，马相当于有64种状态，马走日字，因此可以构建一张64个顶点的图，顶点间通过日字是否可达来连接，使用BFS即可得到最短路径【不必将所有顶点的边都构建好，只需要在马走到这个点时，将可能的8种情况都判断一下（是否可达，是否已经到达过）】。

**在前面就体现了BFS可以搜索得到最短路径的效果**，DFS一直走到底，因此显然不能用于最短路径搜索

### :star:搜索问题的特征-使用图解决

**:star:重要**

![image-20220417144626713](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417144626713.png)

![image-20220417144826393](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417144826393.png)

### Ex Dividing Oil

![image-20220417150808376](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417150808376.png)

![image-20220417150825254](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417150825254.png)

**使用二元组(S,R)即可表示状态，原因是总和10kg油不会少**，已经知道S，R中的油量，那么T中的	油量也可以确定了

![image-20220417150840290](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417150840290.png)

这里1中只有7kg满为条件，而没有10kg空，是因为总共10kg，如果要10kg空，那么只能是3kg油在3kg的瓶子里，7kg油在10kg瓶子里，那么7kg瓶子满时，10kg瓶子也空，而如果3kg瓶子里面不是3kg油，那么10kg瓶子不会空，只会是7kg瓶子满

**因此只要看7kg瓶子满作为条件接口**

**2，3，4同理，都只需要考虑一种情况**【否则总共6种倒油顺序，每个顺序考虑两个瓶子的情况，总共会有12种情况】

![image-20220417151346122](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220417151346122.png)

要输出需要记录节点的父节点，这样当找到时才能直接通过往回遍历父节点来将结果输出