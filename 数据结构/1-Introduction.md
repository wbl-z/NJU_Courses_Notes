# Introduction

## Main Idea
- **Data 数据：一种信息的载体。**
  1. 数字(numbers)、符号(symbols)、字符(characters)的集合。
  2. 可以用于形容客观的事物。
  3. 这些符号可以被输入进计算机，并被计算机程序辨识与执行。

* **数据两种类型：**
  1. numerical data 数字数据：int, float, complex
  2. non-numerical data 非数字数据：char, string, graph, voice

- **Data Structure 数据结构：**
  1. 一堆数据的集合，同一集合的数据之间有某种关系。
  2. {D, R}：D为数据对象，R表示数据集的关系
* **数据结构两种类型（以连接方式）：**
  
  1. linear structure 线性结构
  2. non-linear structure 非线性结构：树、图
  
* **数据结构涉及方面：**
  
  1. 逻辑结构——抽象数据类型，用户视角(ex: 线性表（`将具有“一对一”关系的数据“线性”地存储到物理空间中，这种存储结构就称为线性存储结构`）），是面向问题的
  2. 物理结构——实现数据类型，具体实现视角(ex: linked list, array)，是面向计算机的
  3. 相关操作及实现。
  
  > ![image-20211224155028937](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20211224155028937.png)
  >
  > 1.逻辑结构：
  >
  > 所谓逻辑结构就是数据与数据之间的关联关系，准确的说是数据元素之间的关联关系。
  >
  > 注：所有的数据都是由数据元素构成，数据元素是数据的基本构成单位。而数据元素由多个数据项构成。
  >
  > **逻辑结构有四种基本类型：**
  >
  > - **集合结构**：集合结构中的数据元素除了同属于一个集合外，它们之间没有其他关系。
  > - **线性结构**：线性结构中的数据元素之间是一对一的关系。
  > - **树状结构**：树形结构中的数据元素之间存在一对多的层次关系。
  > - **网络结构**：图形结构的数据元素是多对多的关系。
  > - **也可以统一的分为线性结构和非线性结构。**
  >
  > 2.物理结构：
  >
  > 数据的物理结构就是数据存储在磁盘中的方式。官方语言为：数据结构在计算机中的表示（又称映像）称为数据的物理结构，或称存储结构。它所研究的是数据结构在计算机中的实现方法，包括数据结构中元素的表示及元素间关系的表示。
  >
  > **而物理结构一般有四种：顺序存储，链式存储，散列，索引**
  >
  > 这样的话链式存储结构的数据元素存储关系并不能反映其逻辑关系，因此需要用一个指针存放数据元素的地址，这样子通过地址就可以找到相关数据元素的位置。

## Data Type 数据类型
- **定义：**值(value)与能对值进行计算的操作符的集合。

- **两种类型：**
  1. 原子数据类型——int, float, double……
  2. 结构数据类型——array, struct,……
  
- **Abstract Data Type ADT 抽象数据类型：**

  Abstract: is a method used to hide the information.

  1. 是将类型和与这个类型有关的操作集合封装在一起的数据模型。
  2. 将数据类型的使用与它的表示（机内存储）、实现（机内操作的实现）分开。更确切的说，把一个数据类型的表示及在这个类型上的操作实现封装到一个程序模块中，用户不必知道它。

- **OO Object-Oriented 面向对象：**
  1. 封装、继承、多态
  2. Object 物件：Attribute values(属性) + Operation(操作)
  3. 根据阿汤哥所说，面向对象的概念其他课会考，这里不专门考。

## Program v.s. Algorithm 程序与算法
- **Program 程序：**
  1. 由可通过计算机执行的语言描述。
  2. 不能满足有限性。（程序可以无穷的执行下去（如死循环），但算法必须是有限步骤的）
- **Algorithm 算法：**
  1. 描述解决问题的方法。
  2. 可以是多种语言表达。

## Recursion 递归

* **定义：**将算法表示为重复运算的逻辑
  1. Basis cases 基本条件
  2. Induction cases 递归条件

## **Generic Objects 泛型**

* **两个问题：**
  1. 向下转型。(java5以后支持泛型类< AnyType >)
  2. 原始类型 boolean, short, char, byte, int, long, float, double。可使用wrapper来代替。int -> Integer



