# 17 DFS-on-undirected-graph

![image-20220411113214570](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411113214570.png)

example1相当于找割点，example2相当于找割边

![image-20220411113404268](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411113404268.png)

无向图中（以邻接表来表示）一条边会被处理两次

![image-20220411114548205](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411114548205.png)

**无向图中没有CE边**，因为在有向图中之所以有CE，是因为有v→w的边，而访问w时，没有w→v的边，所以w被访问后，再访问到v时发现w已经被访问了。而在无向图中，v—w是无向的，因此访问w时肯定会把v访问掉

**BE包括两种情况**：第一种是返回到直接的父亲节点，这是第二次访问这条边（**因为第一次是TE访问过了**，所以我们不关注）；第二种是返回到其他的祖先，这是第一次访问这个边

**FE/DE不存在**：因为如果存在FE，那么说明祖先v和子孙w，w已经被访问结束了，那么说明访问w时，肯定会访问到这条FE，**因此它是BE**，作为FE是这条边第二次被访问，因此也不关心

![image-20220411114705032](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411114705032.png)

通过传入当前DFS节点的父亲节点，**来区分出BE的两种情况**，忽略掉返回到直接父亲的情况

![image-20220411115133390](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411115133390.png)

![image-20220411115152300](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411115152300.png)

## Example 1 Biconnected Component 二连通分量

![image-20220411115451810](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411115451810.png)

**二连通**：去掉无向图中任意一个顶点及其连接的所有边，图仍然连通

**二连通分量**：图中的极大二连通子图

![image-20220411115622018](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411115622018.png)

二连通分量是对图的**边的分割**，而顶点会重复

**要找到二连通分量，关键是要找到割点，通过割点重复将图分开，那么得到的便是没有割点的二连通图**

> 割点是无向连通图中的一个特殊的点， 删去中这个点后， 图不再联通， 而所有满足这个条件的点所构成的集合即为割点集合。

![image-20220411120443379](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411120443379.png)

![image-20220411160343117](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411160343117.png)

只要有一个子树满足即可，去掉这个点，这个子树就和整个树分离了

### Principle

![image-20220411162433412](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411162433412.png)

使用一个局部变量back来记录v所能往上到达的最上面的点的discoverTime，体现了v和v的子孙所能往上达到的最远距离

discoverTime越小，说明发现的越早，越往上

![image-20220411161819778](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411161819778.png)

- 第一次发现v时（也即对v进行DFS时），将其back设置为v的发现时间即可，**因为目前来说v往上只能访问到自己**（*注意不能通过树边访问，那样肯定能到达最上面，而是通过Back Edge访问*）
- BE：比较v.back和现在的BE指向的z的发现时间，是v出发的BE
- TE：是v→w，从w访问完返回v时，得到的w的back，如果它更小，那么说明从下面subtree可以BE往上到更高的地方，而v可以到达subtree，因此v能访问到的更高的地方可以通过子树的BE到达

**因此v.back反映了v和它的所有子孙所能往上到达的最高点**

![image-20220411162452878](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411162452878.png)

在TE：v→w从w返回v时，如果w.back≥discoverTime(v)，说明w所能到达的最上面最多为v，因此如果v去掉，那么w及其子树全部会与整个树脱离，**因此v是割点**

### Demo

![image-20220411163206952](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411163206952.png)

![image-20220411163215176](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411163215176.png)

![image-20220411163222431](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411163222431.png)

![image-20220411163229466](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411163229466.png)

注意是**DFS**，因此要深度走到底再往回

### Algorithm

![image-20220411164318273](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411164318273.png)

容易发现，**一个二连通分量中的边在DFS中是被连续访问的，即可以用栈来存储**，当发现割点时，将边全部弹出，直到当前判断割点的这条边（也要弹出），即得到了一个二连通分量的所有边

**但注意，此算法无法判断root是不是割点：因为对于根节点，它的discoverTime一定比≤任何节点，所以不论它是不是割点，从其他节点返回到root，都会形成二连通分量**

但**最终一定**可以得到**多组边**，**每组边构成的图都是二连通分量**

![image-20220411170549959](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411170549959.png)

但显然，**如果root有两个或多个子树**，那么删去root，肯定会导致不连通，**是割点**，因此只要判断**从root出发是不是有两个及以上的tree edge即可**，如上demo，A只有一个TE，因此，它不是割点

> 可以在代码中记录树边的个数，并判断当前dfs是不是对root进行的（通过判断discovertime是否为1），如果树边>1，那么root是割点，反之不是

![image-20220411170735602](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411170735602.png)

### Proof of Algorithm

![image-20220411171334783](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411171334783.png)

![image-20220411171437090](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411171437090.png)

![image-20220411171444501](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411171444501.png)

![image-20220411171451398](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411171451398.png)

![image-20220411171539177](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411171539177.png)

- **二连通就是将边划分成等价类**
- **连通是是将顶点划分成等价类**

## Example 2 Edge Biconnected 边二连通

![image-20220411172159820](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411172159820.png)

边二连通：去掉任何一条边，图仍然是连通的

- **一个二连通图绝大多数情况为边二连通**，因为去掉一个顶点及其边肯定比只去掉一条边的影响大

  **除了一种情况，如上，只有一条边的情况**，去掉任意一个顶点，仍然是连通的，但去掉这条边，图不再连通

- **一个边二连通一般来说都不是二连通的**

![image-20220411172524397](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411172524397.png)

**桥的第二个定义更好理解，如果uv是桥，那么u和v仅仅通过uv这条边相连**，如果还有其他路径，那么就构成环了

![image-20220411172626547](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411172626547.png)

BE一定不是桥，因为BE的存在会和TE构成环

**所以桥一定在TE之中**

![image-20220411172809163](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220411172809163.png)

和Example 1一样，**只是判断时将≥改成了＞**，因为如果等于，那么子树中就有指向u的了，v可以通过这条路径到达u

