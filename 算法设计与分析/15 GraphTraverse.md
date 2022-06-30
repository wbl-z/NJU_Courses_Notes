# 15 GraphTraverse

![image-20220405201957157](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220405201957157.png)

前面的算法中不包含关系，即不包含需要我们人为维护的关系，注意：**大小关系不需要维护，而是数据内在存在的**

没有特殊说明，均指简单图：**既不含平行边也不包含自环的图称为简单图**

![image-20220405202347467](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220405202347467.png)

![image-20220405202512763](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220405202512763.png)

如果没有特殊说明，图**均由邻接表的形式存储在计算机中**

无向图中一条边会被**保存两次**

仅通过**邻接表无法判断是有向图还是无向图**，有向图也可以通过两点之间都有2条边来实现和无向图的邻接表相同

![image-20220405203142785](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220405203142785.png)

DFS和BFS代表了图遍历的两种极端

## DFS

![image-20220405204751989](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220405204751989.png)

每个顶点包含3个状态：undiscovered，discovered，finished，只有这个顶点下面的所有顶点都被访问过后，才把这个顶点置为finished

### **应用：寻找连通分量**

无向图——连通图——连通分量

> 在无向图![img](https://bkimg.cdn.bcebos.com/formula/119e0aec626516e7abf1bd4271d87616.svg)中，若从顶点![img](https://bkimg.cdn.bcebos.com/formula/b08055b8f59ae5dd6e586b540f1bc0d3.svg)到顶点![img](https://bkimg.cdn.bcebos.com/formula/00ec333868e64468ba1b4a05dec1b21e.svg)有路径（当然从![img](https://bkimg.cdn.bcebos.com/formula/00ec333868e64468ba1b4a05dec1b21e.svg)到![img](https://bkimg.cdn.bcebos.com/formula/b08055b8f59ae5dd6e586b540f1bc0d3.svg)也一定有路径），则称![img](https://bkimg.cdn.bcebos.com/formula/b08055b8f59ae5dd6e586b540f1bc0d3.svg)和![img](https://bkimg.cdn.bcebos.com/formula/00ec333868e64468ba1b4a05dec1b21e.svg)是连通的。

有向图——强连通图——强连通分量

> 有向图![img](https://bkimg.cdn.bcebos.com/formula/119e0aec626516e7abf1bd4271d87616.svg)中，若对于![img](https://bkimg.cdn.bcebos.com/formula/e360e4dac4fd991d6ae5cdde450e580e.svg)中任意两个不同的顶点![img](https://bkimg.cdn.bcebos.com/formula/b08055b8f59ae5dd6e586b540f1bc0d3.svg)和![img](https://bkimg.cdn.bcebos.com/formula/00ec333868e64468ba1b4a05dec1b21e.svg)，都存在从![img](https://bkimg.cdn.bcebos.com/formula/b08055b8f59ae5dd6e586b540f1bc0d3.svg)到![img](https://bkimg.cdn.bcebos.com/formula/00ec333868e64468ba1b4a05dec1b21e.svg)以及从![img](https://bkimg.cdn.bcebos.com/formula/00ec333868e64468ba1b4a05dec1b21e.svg)到![img](https://bkimg.cdn.bcebos.com/formula/b08055b8f59ae5dd6e586b540f1bc0d3.svg)的路径，则称![img](https://bkimg.cdn.bcebos.com/formula/119e0aec626516e7abf1bd4271d87616.svg)是强连通图。

![image-20220405205017648](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220405205017648.png)

输入是一个**对称有向图，也即无向图**（*否则以此算法，将找不到连通分量，比如有的顶点间只有一条边a→b，而从某个顶点出发的DFS到达b，那么会导致b变成黑色，从其他顶点出发到达a时，不会去b，从而a和b不是一个连通分量，这显然是错误的*）

输出cc[1..n]，即每个顶点所属的连通分量的编号

ccDFS中第一个v表示从v出发，第二个v是指所有v可以到达的顶点所在的连通分量的编号，**即用第一个找到的顶点作为这个连通分量的编号**

![image-20220405205546560](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220405205546560.png)

![image-20220405210410722](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220405210410722.png)

**复杂度是Θ(m+n)**【其中while循环会遍历一个顶点所有的边，最终会**不重复地遍历**整个图中**所有的边**】，m为边的条数，n为顶点个数，在图遍历中，这也是线性时间复杂度

### DFS tree

![image-20220405211148226](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220405211148226.png)

DFS树不是唯一的，取决于从哪个顶点出发

![image-20220406091101020](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406091101020.png)

**TE构成一棵生成树**

<img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406091203773.png" alt="image-20220406091203773" style="zoom:50%;" />

<img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406091215933.png" alt="image-20220406091215933" style="zoom:50%;" />

<img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406091224502.png" alt="image-20220406091224502" style="zoom:50%;" />

### Generalized DFS

![image-20220406091452315](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406091452315.png)

![image-20220406091730742](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406091730742.png)

外部循环，保证每个点都会被访问，所有连通分量都能被找到

![image-20220406091947019](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406091947019.png)

蓝色区域是可以根据情况修改的部分，**其他非蓝色部分是固定的框架，无需更改**

其中DFS不一定需要返回值，视情况而定

![image-20220406092546976](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406092546976.png)

![image-20220406092921833](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406092921833.png)

parent记录每个顶点的父节点是谁，如果是在最开始的循环中首先访问的，那么parent[v]=-1

![image-20220406092929646](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406092929646.png)

time应当是全局变量，或者在传递time时应当传递time的引用

![image-20220406093130854](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406093130854.png)

可见CE边上的两个顶点的时间不会有任何重合

![image-20220406095025113](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406095025113.png)

![image-20220406095305295](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406095305295.png)

没有父亲孩子关系的节点的时间不会重合：如果在两个连通分量中，一定成立；如果在一个连通分量中，那么两者必定存在相同的祖先（树的性质），即有c→v和c→w的路径，取两条路径上c的后继y，z，那么那么y，z一定时间不相交，因为根据算法，先访问完y，才访问z，而v和w分别是y，z的孩子，因为根据性质一，满足包含关系，所以v，w也不相交

![image-20220406095710452](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406095710452.png)

因此通过时间区间关系就可以知道顶点之间的关系

![image-20220406095801007](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406095801007.png)

vw是有向的，v→w，因此w的活动时间一定在v之前，所以在v准备通过v→w访问w时才发现已经访问过了

### white path theorem

![image-20220406100626071](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406100626071.png)

**白色路径定理**：w是v的子孙当且仅当访问到v时，存在一条除v外都是节点white的路径v→w

![image-20220406101248881](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406101248881.png)

数学归纳法，**找一个中间节点**

## BFS

![image-20220406101553702](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406101553702.png)

![image-20220406101610682](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406101610682.png)

![image-20220406101617324](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406101617324.png)

**BFS不存在递归**，只是把所有节点的子节点全部入队，然后逐个出队重复这个过程

![image-20220406101625242](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220406101625242.png)

DFS有两次处理机会：第一次是对这个节点进行DFS的时候，如*连通分量中利用这次处理标记节点所属的连通分量(这个信息由调用DFS的节点传递)*；第二次是finished时，因为DFS由递归实现，因此每次子节点DFS回来时可以进行处理，如*统计子节点个数*

BFS仅有一次处理机会：因为BFS不需要用递归，而是while循环+队列实现，因此在每次出队时，可以对此节点进行处理，注意入队时只是把节点标记为grey，并不是对这个节点处理，当节点出队时才是对它的处理，即出队和DFS中的第一次是一样的，但由于不是递归，出队后就再也不会访问这个节点了，因此没有DFS的第二次处理机会。

BFS也可以用于获取连通分量，但是在一个节点出队后将其子节点入队时把子节点的连通分量设置为与这个节点一致
而DFS是每次对一个节点进行DFS时设置所属的连通分量

**因此DFS研究得更多，意义更大，后续主要以DFS为主**

