# 20 Greedy-MST

![image-20220425141820236](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425141820236.png)

## Greedy Strategy

![image-20220425144706949](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425144706949.png)

由三个因素组成优化问题：**candidates[候选项],constraints[限制条件],optimaization[最优化结果]**

![image-20220425155811601](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425155811601.png)

贪心算法并不总是最优的。

![image-20220425160303976](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425160303976.png)

feasible 可行的，必须能够满足限制

local optimal 关注当前最优，而不管未来

irrevocable 不可逆转的，即如果选择了，那么后面就不能去掉

## MST

![image-20220425160556386](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425160556386.png)

- 顶点的最近邻是与顶点相邻距离最短的点
- 顶点集合的最近邻是与集合中与某个顶点距离最短的点

![image-20220425161327209](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425161327209.png)

### Graph Traversal

![image-20220425161539614](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425161539614.png)

图遍历的过程就会生成一棵树，DFS树和BFS树，但图遍历不能保证得到的树是MST

可见图遍历的信息不足以找到最小生成树，即要找到MST，其复杂度肯定不比图遍历低

![image-20220425161932587](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425161932587.png)

两个算法在 select 和 check 分别是两个极端

### Prim

![image-20220425162201790](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425162201790.png)

对于一个顶点，它的权重为这个点与当前生成树所连接的边中最小的，如 A,B 为当前生成树，G 有两条边与之相连，故取最小的为 3，即权重为 3

**因此每次只要找到所有可能增长的节点中权重最小的节点即可**

并且加入 G 后，对于原先在 Fringe 中的节点，**如果与 G 没有边，那么它的权重不需要改变，如果有边**，那么比较原来的权重和现在的边的大小即可更新权重。**即要检查G的邻居中不在MST中的顶点**

![image-20220425163218697](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425163218697.png)

使用**优先队列**可以很好地满足我们在Prim算法中的需要

![image-20220425163425088](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425163425088.png)

其中 updateFringe 与边的数目有关，最多只会执行m次

![image-20220425164713206](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425164713206.png)

![image-20220425164721370](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425164721370.png)

- 如果图比较稀疏【使用堆实现优先队列】，即边的数目少，那么后者复杂度低
- 如果图很密集【使用数组实现优先队列】，即边的数目很多，那么前者更好

#### Proof

![image-20220425164854211](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425164854211.png)

MST 是权重和最小的树，这个定义不利于对算法的证明，因此引出下面的 MST 的另一个定义

##### Step1

![image-20220425165118740](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425165118740.png)

![image-20220425165954717](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425165954717.png)

Definition: 一个图 G 的生成树[并非最小] T 拥有 MST 性质当且仅当将图中**不在 T 中的一条边 uv 加入后**（在树上加边肯定会形成环）， **uv 的权重一定是这个环中权重最大的边之一** 

**Lemma 1: All the spanning trees[这里指所有可能的生成树] having MST property have the same weight.**

##### Step2

![image-20220425170105922](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425170105922.png)

##### Step3 [证明过程不做要求]

**第一种证明**

![image-20220425171027872](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425171027872.png)

v 是新加入的顶点

第二种更容易理解：

**第二种证明**

![image-20220425172540345](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425172540345.png)

![image-20220425172916292](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425172916292.png)

选出的最小生成树 U 是具有最大ES前缀的 MST ， ES 中边的顺序是根据 Prim 算法选择加入的边的顺序，因此**最大前缀**即在 U 中包含尽可能多的 e~1~\~e~i-1~，但是不包含 e~i~ ，这样的 U 一定是唯一的，不会有多个

把 xy 加入 U ，一定会形成一个环，上面的 W 是 e~1~\~e~i-1~ 组成的点的集合

### Kruskal

![image-20220425173904373](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425173904373.png)

![image-20220425174009187](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425174009187.png)

![image-20220425174016581](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425174016581.png)
F 是 MST 的边的集合，一共需要加入 n-1 条边，如果逐步取出来的最小权重的边不会形成环，那么就加入F，否则不加入，直到取满 n-1 条边

使用优先队列(堆)或者直接排序，复杂度都是 mlogm，这里的有优先队列中存放的是**边**

![image-20220425174235602](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425174235602.png)

![image-20220425180021055](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425180021055.png)

一方面根据 MST property e 会大于等于环中的任意一条边，而由于 Kruskal 是贪心的，e 一定会小于等于在 T 中但不在 F^(k)^ 的边，由于 T 不包含 F^(k)^，因此至少在环中至少有一条边满足在 T 但不在 F^(k)^ 因此至少有一条边 e' 与 e 的权重相同，那么删去 e' 加上 e，又形成了一个 MST 而这个 MST 就是包含了 F^(k)^ 的

![image-20220425174250521](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220425174250521.png)

- 如果图比较稀疏，即边的数目少，那么使用 Kruskal 复杂度低
- 如果图很密集，即边的数目很多，那么使用 Prim 更好

