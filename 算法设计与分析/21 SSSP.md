# 21 SSSP

## MCE 框架

![image-20220502161906946](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502161906946.png)

Prim 和 Kruskal 都可以看作是 MCE 框架特例

![image-20220502162122479](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502162122479.png)

**对于连通无向图**，才讨论 cut 切

![image-20220502162138826](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502162138826.png)

**跨越切 cut 的边**，即两个顶点分别在 V~1~ 和 V~2~ 中。其中权重最小的跨越切的边，称为 **MCE** *Minimum-weight Cut-crossing Edge*

因为图是连通的，**所以跨越切的边一定存在，至少有一条**

MCE 可能不唯一，可能有权重相同的最小权重的边

### 定理

![image-20220502162555965](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502162555965.png)

**定理:** 对于边 e，如果存在一个 cut 使得 e 是这个 cut 的 MCE，那么 e 一定在某个 MST中

**证明**：如上图

### General Framework for MST

![image-20220502163139269](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502163139269.png)

![image-20220502163244934](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502163244934.png)

可见对于 Prim 算法的当前 MST 和剩下的顶点就构成了一个 cut，每次从这个 cut 中找到 MCE，而根据上面的定理，这个 MCE 一定属于某个 MST



![image-20220502163545262](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502163545262.png)

## SSSP on Undirected Graph

![image-20220502163845027](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502163845027.png)

### Dijkstra

类似 Prim 算法，复杂度也一致

![image-20220502164430610](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502164430610.png)

![image-20220502165327449](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502165327449.png)

#### Proof

用数学归纳法，然后在递推时根据不可能通过其他更长的边经过其他顶点到达 v 比当前最短的边到达 v 来的路径更短

#### CompareToPrim

![image-20220502170017395](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502170017395.png)

![image-20220502170122160](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502170122160.png)

### The Dijkstra Skeleton

可见上面的算法是一个框架，抽象出这个框架可以解决其他问题，如下

![image-20220502170234800](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502170234800.png)

#### Solve SSSP + node weight constraint 

不仅**边上有权重，而且顶点上也有权重**

![image-20220502171232083](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502171232083.png)

只要在原来的基础上去加上顶点的权重即可

#### Solve the “pipe problem” (Maximize the min edge weight) 

管道问题：让从 s 出发，路径上最小权重的边最大。即可以理解为铺管道，此时的边权重为管道的容量，要让限制整个路径的流量的最小容量管道最大化，从而让每个点都能尽可能得到大的流量

![image-20220502171750236](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502171750236.png)

上面两个不一样的地方，因为这时候顶点的 weight 记录的是到这个顶点的路径上权重最小的边，因此 min，同时因为要得到 maximum，**因此当新的权重比当前大的时候，才更新**。

#### Solve “electric vehicle problem" (Minimize the max edge weight) 

这里的 weight 是道路的拥堵情况，要让路径上最堵的那条路尽可能不堵。和上面一个问题刚好相反，因此只要取 max，以及在小于的时候更新即可

![image-20220502172111093](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502172111093.png)

## SSSP on DAG

![image-20220502172721778](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502172721778.png)

按照**拓扑序遍历**，就一定可以保证遍历到 u 时，所有到 u 的路径已经被访问过了，此时 u 的 distance 一定是最小的

可以用数学归纳法来证明：即证明 u 不可能有指向按拓扑序排在 u 前面的顶点。因为结束时间越晚的点有更小的拓扑数，对于 u 出发的边：①不可能是 BE，否则有环，而 BE 指向的是还没结束的灰色节点，即在拓扑排序中排在 u 前面的。②对于 TE，DE，CE，显然 u 指向的顶点一定会比 u 早结束，所以会排在 u 后面，所以 u 一定只会有指向排在后面顶点的边

![image-20220502172834847](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502172834847.png)

即使有负权重，但由于**无环且按照拓扑序**，也不会出错。原理同上面的证明可以理解

## Greedy Algorithm On Other Problem [except graph]【期末不考】

### Scheduling Activities![image-20220502175533865](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502175533865.png)

![image-20220502175612153](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502175612153.png)

可见**三种贪心方式**在安排活动的问题上**都不正确**

#### Algorithm

![image-20220502175814612](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502175814612.png)

按照**完成时间来贪心**是正确的，先按完成时间从早到晚排序，逐个选择完成时间最早的，如果后者与已选择的冲突，那么丢弃。

#### Prove

![image-20220502180117092](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502180117092.png)

如果两个任务的完成时间相同，那么丢弃一个开始时间早的就行了，因此最终完成时间严格小于

![image-20220502180839697](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502180839697.png)

将存在的最优解也按照结束时间从小到大排序

只要能证明贪心得到的数目和最优解的数目一致即可

先证明一个 lemma

![image-20220502180941822](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502180941822.png)

因为 j~i~ 和 j~i-1~ 相容，而 g~i-1~ 的结束时间 ≤  j~i~，所以 j~i~ 和 g~i-1~ 肯定也能相容，**而由于贪心算法，g~i~ 是能与 g~i-1~ 相容的活动中结束时间最早的那个**，因此 f(g~i~) ≤ f(j~i~) 

再根据 lemma 证明

![image-20220502181006167](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220502181006167.png)

