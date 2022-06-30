# 16 DFS-on-directed-graph

![image-20220406145543337](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406145543337.png)

DFS在有向图中的3个应用：对DAG有向无环图：拓扑序、关键路径；对一般是有向图：强连通分量

![image-20220406150030710](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406150030710.png)

根据白色路径定理，在v6变成灰色时，不存在v6到v4的白色路径，因此v4不是v6的子孙

## Topological Order

**只有有向无环图才有拓扑序**

![image-20220406150300337](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406150300337.png)

有向图中要形成一个有向的环才是有环的，如果不是有向的环则不是环

![image-20220406150623870](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406150623870.png)

![image-20220406151019740](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406151019740.png)

reverse逆拓扑序，即**起点的拓扑数大于终点的拓扑数**

![image-20220406151233799](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406151233799.png)

topoNum是递增的整数，用于生成拓扑数分配给每个顶点，**如果是逆拓扑序，那么topoNum从0开始增，如果是拓扑序，那么topoNum从n+1开始减**

![image-20220406152137117](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406152137117.png)

**更早被发现的顶点拥有更大的拓扑数（事实上应该是更晚结束的节点有更大的拓扑数）**，因此可以在之前**记录finished time的地方记录拓扑数**

下面是证明

![image-20220406152650031](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406152650031.png)

不可能存在后向边，否则从一个点出发还能回到这个点，那么说明是存在环

而对于其他类型的边vw，如TE，显然finished time v>w；DE和CE也显然，在仍在访问v时发现w已经被访问过了，说明w比v结束的早

但是不能用发现时间作为拓扑数，因为对于CE而言，vw中w已经被访问过并且由于不是前后继关系，w一定比v更早被访问了，是w被访问完后回到上级节点后再去访问v的

![image-20220406153711916](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406153711916.png)

### example

![image-20220406153922753](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406153922753.png)

选择任务问题，和课程先修问题一样，事实上是拓扑排序

![image-20220406153929950](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406153929950.png)

三个数字分别为开始时间，完成时间和拓扑数

## Critical Path

同理**有向无环图**

![image-20220406154618951](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406154618951.png)

关键路径限定了整个任务的最短时间

满足3个条件： **①path的第一个点没有依赖②path上的每一个点的最早开始时间等于前一个点的最早结束时间③path的最后一个点的最早完成时间是所有点最早完成时间的最大值**

![image-20220406154930115](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406154930115.png)

![image-20220406155119908](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406155119908.png)

![image-20220406155245091](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406155245091.png)

将vw边上w的时间作为vw的权重，并且在入度为0的顶点处增加一个done的状态

那么我们只要能求出所有顶点的est即可，再根据duration即可得到eft

利用DFS，当然不一定是从4开始的，比如可能从3开始。最开始假定所有顶点的est都是0，开始DFS，比如从3开始→7→9，从9返回到7，此时7和9的est为0，9的est+权重0，和7的est比较取较大值，故7的est为0，返回3，3的est=0与7的est+0.5比较*【实际上就是将3的est和7的eft比较】*，故3此时的est为0.5，继续DFS 3的其他后继节点，最终得到3的est=4.5

![image-20220406160825311](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406160825311.png)

![image-20220406161018030](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406161018030.png)

对于TE，需要DFS子节点，得到eft来更新est

对于DE，CE由于已经被访问过，有了eft，所以直接将eft用于更新est即可

![image-20220406161056765](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406161056765.png)

critDep是指一个节点关键依赖于哪个节点，如前面的3是关键依赖于5，**即一个节点的est和哪个后继节点的eft相同**

![image-20220406161356331](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406161356331.png)

![image-20220406161404753](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406161404753.png)

![image-20220406162740914](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406162740914.png)

## Strongly Connected

对于**一般的有向图（可以存在环）**

![image-20220406163213659](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406163213659.png)

![image-20220406163225555](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406163225555.png)

将强连通分量收缩成一个点，就形成了收缩图

注意**两个强连通分量之间的边的方向是一致**的（*即两个连通分量的顶点之间要么没有边，如果有边，方向是一致的*），比如ABDF都是指向C的，如果不是一致的，那么说明ABDF不是强连通分量，即C可以加入到ABDF中一起构成强连通分量。**因此收缩图中可以将两个连通分量之间的边收缩成一条边**

并且**收缩图一定是无环的**，如果有环，那么它们一起构成更大的连通分量。**因此任何一个图都可以看成是连通分量的有向无环图**

### properties

![image-20220406164057724](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406164057724.png)

对一个点v使用DFS，会遍历所有从v可以达到的点后才停止

**SCC**指strongly connected component，**sink SCC** 【*不一定只有一个*】**指在收缩图中只有入度没有出度的强连通分量**，即**汇点**

==**在sink SCC中的任意点使用DFS，可以得到sink SCC这个连通分量**==，因为其中的点不存在到其他连通分量的边，因此根据v遍历得到的一定是一个强连通分量

![image-20220406164745855](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406164745855.png)

在收缩图中只有出度没有入度的连通分量是source  SCC(strongly connected component)**源**【*不一定只有一个*】

==**拥有最晚结束时间的点一定在source SCC中**==，因为如果不在这里面，而是在具有入度的连通分量V中，那么从其他指向这个连通分量W的点开始的DFS的结束时间肯定比在V中开始的DFS的结束时间晚，因为从W开始的会到达V，时间一定是V的最晚时间加上在W中的时间*（当然注意最外层循环在遍历时不一定刚好从source开始，可能从V开始，那么W的持续时间不一定比V大，因为V已经DFS结束了，但显然W在V结束后才进行DFS，W的完成时间还是比V晚）*

### algorithm

![image-20220406170441583](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406170441583.png)

因此结合两条性质，使用转置图——即将所有边的方向更改为相反方向。对整个**转置图**使用DFS，得到最晚的完成时间的点，一定在转置图的source SCC中，而在原图中它为sink SCC，因此对这个点对**原图**进行DFS，结束时即可得到一个强连通分量

然后在转置的收缩图中删除这个强连通分量，那么剩下的连通分量中又会有source SCC，在上面的例子中ABDF，即在第一次DFS的结果中将所有C中的顶点去掉后的最晚结束时间的点，然后重复前面的过程即可【**在算法中只要在最外层循环中对原图所有顶点按照完成时间从晚到早进行DFS即可**，因为之前遍历了的颜色会改变】

![image-20220406171319792](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406171319792.png)

1. 先对转置图进行DFS
2. 按照完成时间从大到小的顺序对**原图**的所有顶点进行DFS

![image-20220406171830752](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406171830752.png)

![image-20220406172043429](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406172043429.png)

注意：不能在原图上用DFS得到的完成时间从小到大访问，这样有时正常有时错误，是不可行的

![image-20220406172534625](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406172534625.png)

