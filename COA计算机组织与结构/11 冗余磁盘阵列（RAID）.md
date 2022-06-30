<h4 align="center">图片来源：南京大学软件学院COA课程PPT</h4>
<h5 align="center">©author:zzb</h5>
<div style="text-align: center"><a href="https://github.com/wbl-z">Github主页</a>  <a href="https://blog.csdn.net/m0_51691879">CSDN主页</a></div> 


# 11 冗余磁盘阵列（RAID）

![image-20211124201947610](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124201947610.png)

![image-20211124202340250](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124202340250.png)

目的：

- 增加容量
- 数据分散在多个磁盘上，并行提高数据传输速率
- 纠错

**逻辑上是一个磁盘，物理上是多个的**，同时**数据是分布在多个物理磁盘**上的，这样才能多个磁盘并行工作来提高效率

 ![image-20211124202714276](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124202714276.png)

## 条带化

### RAID 0

![image-20211124202853383](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124202853383.png)

![image-20211124203104344](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124203104344.png)

**条带化即把一个磁盘/一个组（如后面的10，01，50）分散成多个条带放到不同的磁盘上**

**优点：**

- **大I/O数据传输速率快**，每个物理硬盘都可以传输，所以对于**大**的数据块，可以被拆分成多个部分来传输
- **小I/O响应速度快**，如果是一个硬盘，那么一次只能响应一个请求，而对于多个分布在不同物理磁盘上**小**的数据块，RAID 0则可以同时响应

**缺点：**

- **数据可用性低**，多个磁盘，出现错误的概率大
- **没有冗余检验**

## 镜像

### RAID 1

![image-20211124203828637](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124203828637.png)

![image-20211124204604960](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124204604960.png)

深色的是冗余盘，简单地把原来的数据进行了拷贝

**优点：**

- **数据可用性很高**，如果一个盘坏了，还能找到一个一模一样的盘
- **大I/O传输读比单盘快，而写的速度与单盘差不多**，因为同时要写两个盘，受限于速度慢的磁盘
- **小I/O响应速度比单盘快一倍**，即使两个请求位于同一个盘上，也能同时响应，因为有备份，而RAID0则只能在位于不同盘时同时响应

**缺点：**

- 价格昂贵

![image-20211124205124993](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124205124993.png)

**只用于关键数据，重要数据的保存**

![image-20211124205533673](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124205533673.png)

RAID 01是先进行条带化，再备份分组，如果disk0坏了，那么整个组都不能用了，即disk2和disk1不能联动

RAID 10是先进行备份分组，再进行条带化，这样一组中坏了一个也不要紧，比如disk0坏了，还可以，disk1和disk2联动

**所以RAID 10的容错率更高**

# ？

## 并行存取——解决单次大I/O传输

### RAID 2

![image-20211124210109478](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124210109478.png)

- 不论是大的还是小的I/O请求，要求**所有磁盘都参与**请求的执行。
- 每个磁盘的轴**同步旋转，磁头始终处于同一位置**
- **数据条带很小如一个字节或字**，这样才能让所有磁盘都调动起来，注意这里条带同样是满了才到下一个条带，而不是一个条带用一点，另一个条带用一点，因此要让条带很容易的被装满

![image-20211124210453301](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124210453301.png)

**冗余盘用来存储校验码——海明码**，

4个bit需要3个bit的校验位（8个需要4个），所以4个硬盘需要3个硬盘来校验，并且**校验码就存放在数据对应的位置**

![image-20211124211014816](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124211014816.png)

对于经常出错的情况意义很大，而磁盘事实上本身就有CRC，所以出错概率是很小的，所以RAID 2在这种情况下意义不大。

**事实上，RAID 2已经被弃用了**

### RAID 3

![image-20211124211227554](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124211227554.png)

RAID 中讲冗余，**是为了防止磁盘坏了**，而不是为了防止磁盘出错，关于出错是在纠错中强调的。

出错是可以正常读，错误的位混在数据中，而磁盘坏了这一位就丢失了，不可读了，所以这个是**可以定位错误的**，**因此也可以重构（修复）磁盘坏了的数据**。

如上是偶检验修复损坏的b~0~，奇校验需要多异或一个1，**原理是两边同时异或一个数字，等式不变，所以在校验码计算式子的两边同时异或b~0~和p(b)即可**

![image-20211124211948352](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124211948352.png)

这样的并行存取就是为了大的I/O处理的速度更快，保证任何一次都有所有的磁盘参与进来

但面对多个I/O请求时，由于对于每个I/O请求，所有硬盘都要参与，所以面对多个时，**一次只能响应一个请求**

## 独立存取（实际上即RAID 0加上了校验码）

### RAID 4

![image-20211124212431965](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124212431965.png)

采用较大的数据条带，各个磁盘的操作是独立的

![image-20211124212959982](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124212959982.png)

每次写时，不但要修改数据，还要修改校验位，对于小的I/O写请求，会产生写损失，而在RAID 3中则没有影响，因为条带小，每次都一定要修改校验位，并且直接用写入的数据修改即可，无需取出原有数据。

- 此外经过异或计算，可以发现如上公式，因此如果仅修改**很小的数据如1位**，**修改校验位**，**只需要从原来的数据中取出P(B)和B~i~（要被修改的数据的原来数据）即可（*原理和之前的RAID 3一样，p(b）异或b~i~=剩下所有数据的异或*），B‘是指经过修改的数据**
- 而如果是**整个数据都要修改掉**，则原来的数据已经不重要了，直接用新的数据生成校验码即可
- 因此综上，**在修改大的I/O时，写损失少，而修改小的I/O时，要从原来数据中再读出来后再修改**，这个读的过程造成很多损失

只要涉及写操作，一定要涉及校验盘，所有没法做到各个盘的写是独立的，**校验盘会成为瓶颈**

**RAID 4同样被弃用**，它在设计上有缺陷，即上面所述，在读取操作和一次写操作时都没什么问题，但小I/O存取有瓶颈

### RAID 5

![image-20211124214232259](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124214232259.png)

把校验盘拆散到各个磁盘上，即分布式，**这样不会因为校验盘一个盘产生瓶颈**

RAID 5 **只能坏一块盘**，和前面的一样，在坏一块时可以用其他的来恢复，但坏更多盘时则不能恢复

**当一块数据被修改时，与它同一行、与它的校验块同一个磁盘（列）的数据都不能进行修改、这个不能修改的磁盘上有的所有的校验块对应的那一行也都不能修改*（因为一行中块的修改的修改必须要修改校验块）***

因此，一个块的修改仍然会约束很多的块，没有那么的独立



**两读两写**是指读数据和读校验用于计算新的校验，两写是指写数据和写校验位。

最好的情况就是同时读出两个，同时再写回去，最坏的自然就是两读和两写分开来

![image-20211124215744728](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124215744728.png)

RAID 50的**性能更高，且能坏的盘更多**，只要不是一组内坏多个都能运行(即可以不同组分别坏)，但**容量利用率更低，冗余所需空间更多**（因为每一组都生成了校验码）

### RAID 6

![image-20211124215940852](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124215940852.png)

使用了两个校验码，允许坏两个磁盘，但不能坏三个

但每次写都要影响两个校验码

## RAID比较

![image-20211124220232811](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124220232811.png)

![image-20211124220339171](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124220339171.png)

![image-20211124220441586](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211124220441586.png)

**RAID 0 和 RAID 3适用于高吞吐量的应用**

**RAID 1适合要求高可用性的应用**

**RAID 5是用途最多的，如数据库服务器，各种网络服务器等**

**RAID 6 适合丢失数据严重的应用**

