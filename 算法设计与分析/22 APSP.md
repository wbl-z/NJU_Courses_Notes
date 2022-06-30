# 22 APSP

*All-Pairs Shortest Paths* 

![                                                                                                                                                                                                                                                                        +](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511153843035.png)

## 问题1

![image-20220511154011124](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511154011124.png)

![image-20220511154021302](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511154021302.png)

可达性问题等价于一个自反的**传递闭包**问题

> ![image-20220511155320074](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511155320074.png)

![image-20220511155412621](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511155412621.png)

### Brute Force 1

![image-20220511155714504](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511155714504.png)

将主对角线的值都设为 1，自己到自己一定可达

三重循环顺序是i j k，**i 表示起点，j表示终点，k表示中间节点**，即 i 经过 k 到达 j 是否可以

while循环：当闭包不发生改变时就说明已经全部找到，循环终止

### Brute Force 2

![image-20220511160005114](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511160005114.png)

对每一个顶点，都**枚举所有的边** (x ,v)，每一条边的 x 和 v 都不同

在最坏情况下，m 和 n^2^ 是一样的，因此复杂度还是 O(n^4^)

### Brute Force 3

![image-20220511161646326](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511161646326.png)

**枚举所有的路径长度**，最短为 0，最长为 n-1

最内层循环的复杂度等于**顶点 v 的度数**

### The Kleene-Floyd-Warshall Algorithm

![image-20220511162210813](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511162210813.png)

3 人在不同领域独自发现

![image-20220511162326360](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511162326360.png)

在 BF1 的基础上将 k 的循环移动到最外侧

![image-20220511162646087](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511162646087.png)

#### Proof

![image-20220511163006777](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511163006777.png)

**先证明一半：**

![image-20220511163422088](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511163422088.png)

如果有从 s~i~ 到 s~j~ 的路径，且其中的下标最大的中间节点是 s~k~，那么 r^(k)^~ij~ = true。

用数学归纳法即可得证

**再证明另一半：**

![image-20220511163705613](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511163705613.png)

如果 r^(k)^~ij~ = true，那么存在s~i~ 到 s~j~ 的路径其中间节点最大的下标为 k【也即两点之间的中间节点的下标都一定在 1~k 之间】。

同样是数学归纳法

上面的证明省略了归纳假设，如果 r~ij~ 在第 k 轮才第一次变成了 true，那么根据算法，一定是有 r^(k-1)^~ik~ = true，r^(k-1)^~kj~ = true，才能使得当前 r~ij~ 变成 true，因此就存在着 s~i~->s~k~->s~j~ 路径，根据归纳假设 r^(k-1)^~ik~ 和 r^(k-1)^~kj~ 的中间节点中的最大下标**不超过** k-1，因此 r~ij~ 中间节点的下标不超过 k。

## 问题2

![image-20220511164812997](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511164812997.png)

![image-20220511164822048](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511164822048.png)

**最短路径的性质**：如果存在 x-z 的最短路径包含路径 P 是 x-y 的，路径 Q 是 y-z，那么 P 和 Q 都是对应 pair 的最短路径

floyd 和 warshal 算法几乎一样，只不过把可达性矩阵转换成一个距离矩阵【把 1 替换成边的权重，0 替换成无穷并将主对角线都设置成 0】

![image-20220511165134927](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511165134927.png)

![image-20220511165043237](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511165043237.png)

### Floyd skeleton

![image-20220511170036059](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511170036059.png)

如何将最短路径记录下来？

path\[i][j]=path\[k][j];

把i->j路径上j的前一个顶点设为k->j路径上的j的前一个顶点即可，因为此时是i->...->k->...->j了。path\[i][j]存放这个路径上j的前一个顶点，找路径时和Dijkstra一样，再去这前一个顶点中找到再前一个顶点

## 问题3[Bellman-Ford不考]

![image-20220511171056015](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511171056015.png)

![image-20220511171030443](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511171030443.png)

Dijkstra 算法要求不能有负数边

Floyd 算法要求不能存在权值和为负数的环

Bellman-Ford 算法处理 SSSP，且可以有负权值，并且**能够检测出负数环**

> 【如果有负数环，是找不到 SSSP 的一直在这个环上走，最终出现负无穷】

![image-20220511171532791](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511171532791.png)

![image-20220511172523791](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511172523791.png)

先把所有除了 s 外的 d[u] 都设置为无穷大，然后对**每一条边**进行查看，看这条边能不能更新距离。**一共进行 n-1 轮**，因为路径最长为 n-1，因此最多只会更新 n-1 次

结束后**再对所有边 u,v 进行一次判断，如果 d[v] > d[u] + w(u,v)，那么说明出现了负环**，会在环上绕了一圈，导致原本大的环的起点变成了最小，因此可以通过上面进行判断

```C++
void Graph::BellmanFord(int n, int v){ 
    for(int i=0;i<n;i++){ 
        dist[i]=Edge[v][i];
        if(i!=v&&dist[i]<MAXNUM)
            path[i]=v;// path记录路径
        else 
            path[i]=-1;
    }
    
    for (int k=2;k<n;k++)// n-2次迭代，路径最长为n-1，第一次迭代在上面的循环z已经进行了
        for(int u=0;u<n;u++)// 这里看起来是两个for循环，事实上就是一个对边的集合进行遍历的for循环，如果将所有的边都存在一个数组里面，那么只要一个for循环遍历这个边的数组即可
            if(u!=v)
                for(i=0;i<n;i++)
                    if (Edge[i][u]!=0 && Edge[i][u]<MAXNUM && dist[u]>dist[i]+Edge[i][u])						{
                            dist[u]=dist[i]+Edge[i][u];
                            path[u]=i;
                        }
}
//https://blog.csdn.net/zsx0728/article/details/114685608  这里的代码geng'i'q
```

复杂度：最好为 O(E)【即外层循环仅仅一次就更新完成了】，最坏 O(VE)，平均O(VE)

### Proof

![image-20220511173131383](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511173131383.png)

![image-20220511173138494](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511173138494.png)

即每一轮都能进一步的找到最短路径的下一个节点，最多经过 n-1 轮就一定能找到最短路径

## 问题4（不考）

![image-20220511173844680](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511173844680.png)

![image-20220511173950973](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511173950973.png)

布尔矩阵的相乘就能找到传递闭包，也即可以通过**矩阵相乘**得到**点的可达性**

![image-20220511174149246](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511174149246.png)

传递闭包就是所有 A^p^ 的和

![image-20220511174521390](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511174521390.png)

biwiseOR就是对比特串按位或

![image-20220511174658908](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511174658908.png)

### **矩阵算法**

![image-20220511174830043](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511174830043.png)

### 例子

![image-20220511175032485](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511175032485.png)

在 A 第 i 行中看哪些列 k 是true 的，把这些 k 在 B 中的 k 行都按位或，即可得到 C 的第 i 行

【用矩阵乘法也可以理解是正确的，比如 A 的第二行和 B  第一列相乘得到 a~21~，因为这里的乘就是与，加就是或，因此 A 第二行中的 0 会导致 B 列中相应位为 0，而 0 在后面的加/或中没有影响，因此不用看了；A 的第二行是1，那么与 B 中第一列乘/与之后不会对 B 列原本的相应位产生影响，因此只要看 B 中列相应位即可，而后续加就是或，所以把 B 中在 A 中是 1 的位置的位一起或即可】

------

下面想根据上面的发现将 B 一些行的或的结果提前计算好，减少重复的计算：

![image-20220511181242542](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511181242542.png)

![image-20220511181501658](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511181501658.png)

平均分成 **g** 组

**2^t^-t-1个 union 需要计算，-t 是一行本身不用算，-1 是空集不用算**，因此共 **g(2^t^-t-1)** 次 union

在最终计算时还需要将 g 组各自计算的结果整合在一起，需要 **g-1** 次 union，A 共 n 行，因此总共需要 **n(g-1)** 次union

![image-20220511181556348](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511181556348.png)

is of high order 是指加号左右两边的项哪个占主要地位，令两种相等即可得到 t = logn 是分割线

t ≥ logn 左边占主要，因此只要关注左边式子，让其最小即可，但左边式子随着 t 增大而增大，因此 t = logn 的时候左边式子才最小。

右边同理

**因此通过分组，将代价降低到了 n^2^，而在原来不分组的情况下，需要计算的代价是 2^n^-n-1**

👉因此前面介绍的算法中将复杂度从暴力计算降低能够成功的原因就是消除了重复的计算【这同样也是 DP 的思想】

------

![image-20220511182605207](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511182605207.png)

![image-20220511182625039](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511182625039.png)

bitSeg就是把比特串当作二进制的数来看，并用十进制表示，因此比如 A 中是 1101，那么只要到已经计算好的 allUnion 中取出下标为 13 的即可

![image-20220511182713257](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511182713257.png)

allUnion 的计算只需要迭代的算就行了，每个计算利用前面已经算好的结果，因此一个项的计算每次只需要一次的 union，如计算134，可以用 13 与 4 union

此外对于 allUnion，并不需要将每组的结果都存下来，如果要存，那么每组需要 2^t^ 种结果，共 g 组，即 g*2^t^ 的空间。事实上，只要 2^t^ 即可，因为可以让 A[1]..A[n]都用当前这一组算出C[1]..C[n]，之后就不会再用到了，完全可以将后面的组存放在不再用的组的空间中，节省空间

### skeleton

![image-20220511182822366](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511182822366.png)

使用 g*2^t^ 的空间

![image-20220511191613881](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511191613881.png)

使用 2^t^ 的空间

![image-20220511191708081](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220511191708081.png)

