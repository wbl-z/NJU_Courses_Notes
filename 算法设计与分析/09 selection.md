# 07 selection

## 找到最大/最小的元素

![image-20220320113742972](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320113742972.png)

**找第K大的元素**：先看两个特殊的情况，最大和最小

![image-20220320113847644](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320113847644.png)

证明算法的最优性：该算法的最坏情况复杂度和对于任何一个算法在最坏情况下都至少大于某个值（**即下界，但下界是无穷多的，我们需要找到最紧的下界，其他的下界算法是达不到的，算法最多能达到最紧的下界**）相同

![image-20220320151227429](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320151227429.png)

![image-20220320114144545](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320114144545.png)

基于比较和选择的问题构建出来的决策树一定是**二叉树**，使用决策树来找到问题的lower bound

选择最大值的决策树的叶子节点至少有n个，因为每一个数都有可能。因此树的高度至少是$logn$取上整。**但显然这个bound太松了，也即下限太低了**，无法用于证明算法是最优的（上面的find max算法复杂度$n-1$显然大于$logn$）

![image-20220320120522781](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320120522781.png)

从这样一个角度思考，对于每次比较，较小的那个元素一定不可能是最大的元素，毕竟已经小于另一个元素了，即给较小的元素打上lose的标签，**而一次比较最多只能打上一个lose标签，因此至少要比较n-1次**，才能给n-1个元素打上标签，剩下一个最大值

> 这就是find_max问题的一个紧的下界bound。同时能够证明这就是这个问题**最紧的下界**，因为已经有一个算法的最坏情况为n-1了，因此这个问题的下界不可能比n-1还大

## 对手论证

下面引入对手论证来找到问题的lower bound（**当决策树不便展现全部的结果，或者决策树得到的结果显然过于松散时使用对手论证**）

![image-20220320115415333](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320115415333.png)

假想一个对手，在算法每次要做出决策时（如元素比较，根据大小结果决定接下来的行为），对手会给出这次比较的结果（通过构造输入来实现），使得算法最终要执行的步数更多

**【即如算法此时要比较x~1~和x~2~的大小，对手会给出比较的结果x~1~>x~2~，通过假设x~1~=10，x~2~=5来实现，从而使得后续算法需要比较更多的次数】**

但要注意，对手给出的结果**不能是前后矛盾的**，需要是internally consistent，不能前面给出了x~1~>x~2~,x~2~>x~3~，后面又给出X~1~<x~3~。也即最后整体来看，对手逐渐构建出来的bad input需要是存在的，即x~1~\~x~n~的输入是存在的*（如前面矛盾的结果就不存在这样的输入）*

## 同时找到最大最小元素

![image-20220320142512814](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320142512814.png)

**策略**：先两两分组，进行$n/2$次比较得到**larger key set和smaller key set**，再在这两个集合中分别使用find_max和find_small，从而找到最大和最小

使用对手策略来找到问题的lower bound

![image-20220320143144824](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320143144824.png)

可以知道最大值在所有的比较中肯定没有输过，只有win标签，最小值只有lose标签，而其他的元素既有win也有lose

因此要找出max和min，一定至少需要$n-1$个win+$n-1$个lose才行，即对于任何的算法至少需要**$2n-2$个标签**

![image-20220320143419947](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320143419947.png)

N表示没有标签

**中间一列即对手的反应**，即根据比较前的状态，对手需要尽可能构造大小关系，让这次的**比较得到的信息量最少，从而使得总比较次数增多**

![image-20220320144203671](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320144203671.png)

对于获得两个信息的情况，最多执行$n/2$次，因此可以获得$n$个信息，还需要$n-2$个信息，而其他的情况至多可以获得一个信息，因此至少还需要$n-2$次比较，即**一个下界为$n/2+n-2$**
*（同样结合前面的算法复杂度也为此，故这个下界是最紧的下界）*

![image-20220320145241645](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320145241645.png)

`（对手策略的例子）`

注意在x~3~x~1~比较时让x~3~赢了，此时要调整大小，不能把x~1~=20变小，因为之前它赢过，**调小的话不能保证之前赢过的比较仍然成立（会前后矛盾）**，而是应该把x~3~调大，因为x~3~之前也赢过，调大后仍然能保证之前的比较肯定也是赢的，因此把x~3~调整为25

## 找到第二大元素

![image-20220320145701300](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320145701300.png)

即在第一次find_max中，**只有直接输过给max的元素才可能是第二大元素**，如果输过给非max元素，那么肯定不是第二大元素。

**因此只要找到直接输过给max的所有元素，再在其中找最大值即可找到第二大元素**

![image-20220320150150102](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320150150102.png)

因此，只有$logn$取上整个元素可能是第二大的元素，在其中找到最大的元素，**需要$[logn]上整-1$次比较**

故总共需要<img src="https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320150439856.png" alt="image-20220320150439856" style="zoom: 50%;" />次比较

### 最优性证明

![image-20220320151939077](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320151939077.png)

证明上面的找第二大的算法是最优的：可以构建**对手策略**使得任何的算法中和max比较过的元素个数**至少是$[logn]上整$个**（当然可能情况不好的时候，max和所有元素都比较过）

![image-20220320152309270](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320152309270.png)

- 权重和不变
- 根据对手策略，增加后的权重不会超过原来权重的两倍
- 经过n-1次比较，最后只有max的权重为n，其他都是0

![image-20220320152535644](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320152535644.png)

w~k~(x)表示经过k次比较后，x的权重，注意不一定是x和其他进行比较，可能是其他任意两个元素比较，这样的话，**x的权重值不变**。

因此我们可能考虑仅仅和x进行过的比较次数，**用大K表示**，故有K个数和max比较过，也即有K个数有可能成为第二大元素

递推得到K≥$logn$，即证得与max比较过的元素**至少$[logn]上整$个**

### 如何把与max比较过的元素记录下来

![image-20220320153844371](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320153844371.png)

使用2n-1个节点的堆，有n个叶节点，n-1个内部节点，那么内部节点可以用来存储胜者

## 找到中位数

![image-20220320154455245](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320154455245.png)

把数组分成两部分，S1中的任何元素小于S2中的任何元素。因此**中位数肯定在元素多的那个集合中**

比如9个元素，分成2和7，那么中位数肯定在7中，这时递归的找，但注意不是找7中的中位数，而是$（n+1）/2-2$小的元素

(原来是找$(n+1)/2$小的元素，这时候已经排掉了2个更小的，因此要减去2)

![image-20220320155221212](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320155221212.png)

类似qucikSort，在最坏情况下，每次划分会很不好，复杂度高

### 期望/平均线性时间的选择算法

![image-20220320155408379](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320155408379.png)

==**这里分析的算法适用于找到第K小的元素，但为了便于分析，使用中位数作为分析对象**==

![image-20220320155834775](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320155834775.png)

![image-20220320155811016](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320155811016.png)

当S≤5的时候，直接比较得到反而速度更快，如上面5个元素，只需要6次比较即可找到中位数

#### 复杂度分析

![image-20220320160549040](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320160549040.png)

**平均复杂度是线性时间的**

### 最坏情况线性时间的选择算法

![image-20220320160759754](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320160759754.png)

要想**改进**之前的算法，**那么pivot需要选的好一点，尽可能是中间的情况**

1. 将n个元素按5个元素为一组来分（即图中的一列），对于每一列通过6次比较得到中位数，然后把比中位数大的元素放在上面，小的放在下面，每组最中间的就是中位数*（注意，不一定是刚好从小到大的）*
2. 在第三行的所有元素中找到中位数m\*，然后把第三行元素比m\*小的组放到左边，大的放到右边（*同样注意这不是排序*）
3. **对于B区中的元素一定大于m\*，C区一定小于m\***，A和D不确定

:star: 那么不妨假设总共5(2r+1)个元素，那么m\*左右各有r列，B区=C区=3r+2个元素，A区=D区=2r个元素，**那么在最不均衡的情况下如AC都比m\*小，那么small 共7r+2，large 共3r+2，约等于7:3**

![image-20220320203328691](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320203328691.png)

**![image-20220320162425191](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320162425191.png)**

![image-20220320162506544](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320162506544.png)

注意在S2要多-1，把m\*排除

#### 复杂度分析

![image-20220320163001771](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320163001771.png)

![image-20220320163349040](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320163349040.png)

**递减的等比数列求和后的数量级取决于第一项，因此看第一项即可**

#### 最优性证明

要想找到median，必须要知道其他每个元素和median的关系，否则会出错

![image-20220320163914439](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320163914439.png)

定义**关键比较**，如果一次比较可以确定x和median之间的关系，那么就是关键比较。*如y是≥median的，那么x>y就能确定x>median*

![image-20220320164247049](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320164247049.png)

对于所有的情况，对手策略都使得它变成非关键比较。*如N,N，对手策略让其中一个比median大，一个小，那么就无法确定它们与median的关系*

![image-20220320165026838](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320165026838.png)

![image-20220320165033613](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220320165033613.png)

