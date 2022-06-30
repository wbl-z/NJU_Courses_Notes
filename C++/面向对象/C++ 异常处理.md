C++ 异常处理
---

<!-- TOC -->

- [1. 异常处理](#1-异常处理)
  - [1.1. 处理机制](#11-处理机制)
  - [1.2. catch的用法](#12-catch的用法)
  - [1.3. 异常处理的嵌套](#13-异常处理的嵌套)
  - [1.4. 定义异常类](#14-定义异常类)
  - [1.5. 异常处理的特例](#15-异常处理的特例)
- [2. 使用析构函数来避免造成内存泄漏](#2-使用析构函数来避免造成内存泄漏)
  - [2.1. 异常处理的例子:资源泄露【小动物收养保护中心】](#21-异常处理的例子资源泄露小动物收养保护中心)
  - [2.2. GUI应用软件中的某个显示信息的函数](#22-gui应用软件中的某个显示信息的函数)

<!-- /TOC -->

1. 错误
    1. 语法错误:编译系统检查出
    2. 逻辑错误:测试可以发现
2. 异常 Exception
    1. 运行环境造成:内存不足、文件操作失败等
    2. 异常处理:提示错误信息、终止程序等

# 1. 异常处理
1. 特征：
    1. 可以预见
    2. 无法避免
2. 作用:提高程序鲁棒性(Bobustness)
```c++
void f(char *str) {//str可能是用户的一个输入
    ifstream file(str);
    if (file.fail()) {
        // 异常处理
    }
    int x;
    file >> x;
}
```
1. 在上面的问题中，文件如果不存在，可以让用户重新输入文件名。

    但是重新输入文件名和读入异常不在同一个逻辑内

2. 问题:**发现异常之处与处理异常之处不一致**，怎么处理？在哪里处理?

    函数发现异常时立即处理可能并不总是一个妥当的方式，**有的情况下应该交给调用者处理**，比如在库函数中发生的异常让库函数处理未必是调用者想要的处理

    **因此需要将异常信息告诉调用者**

3. **早期**C/C++常见处理方式:

    1. 函数参数:
        + 返回值(特殊的，0或者1)
        + 引用参数(存放一些特定的信息)
    2. 逐层返回

4. 缺陷:程序结构不清楚

5. 相同的异常，发生在不同的地方，如不同的调用者调用相同的函数都出现异常，**它们需要编写相同的处理逻辑是不合理的**。因此希望能集中处理

6. 传统异常处理方式不能处理构造函数出现的异常【*没有返回值*】

## 1.1. 引入的处理机制
1. C++异常处理机制是，一种专门、清晰描述异常处理过程的机制

2. 函数在执行过程中发现异常可以抛出或继续抛出，直到被捕获，如果在main函数中也没有处理则会终止，显示如下

   ![image-20220608214227727](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220608214227727.png)

3. try：监控

4. throw：发现异常，可以**不处理而是抛掷异常对象给调用者**，程序

5. catch：捕获并处理
```c++
try{
    //<语句序列>
    //监控
}throw//<表达式>，可以是基本类型，也可以是一个类【在java中必须是类】，拷贝构造函数用来拷贝类
catch(<类型>[<变量>]){//变量不重要可以省略
    //<语句序列> 捕获并处理
    //依次退出，不要抛出指向局部变量的指针，退出后局部对象消失，指针变成悬挂指针，解决:直接抛出对象，这样自动进行拷贝，就不会出错了
}
```

## 1.2. catch的用法
1. 类型:异常类型，**匹配规则同函数重载**(精确匹配只有底下三种，其他转换都不允许，**int转double都不行**)
   1. 允许从非常量到常量转换
   2. 允许从派生类到基类转换【*见下面定义异常类的例子*】
   3. 允许数组和函数转换成指针
2. 变量:存储异常对象，可省
3. 一个try语句块的后面可以跟多个catch语句块，用于捕获不同类型的异常进行处理
```c++
void f() {
    throw 1;
    throw 1.0;
    throw "abcd";
}
try {
    f();
}catch (int)// 处 理 throw 1;
{...}
catch(double)//throw 1.0
{...}
catch(char *)//throw "abcd"
//字符串优先解释为char *
{...}     
//如果都没能捕获，会继续往上抛出
```

## 1.3. 异常处理的嵌套
1. 调用关系:f->g->h

```c++
//第二节课10min
f(){
    try{
        g();
    }catch (int)
     { … }
    catch (char *)
    { … }
}
g(){
    try{
        h();
    }catch (int)
    { …  }
}
h(){
  throw 1;   //由g捕获并处理
  throw "abcd"; //由f捕获并处理
}
```

1. 如果所抛掷的异常对象如果在调用链上未被捕获，则继续往上层抛出，直到 main 都没处理，**那么由系统的abort处理，即直接终止**

   ![image-20220608214227727](https://screen-shot.obs.cn-north-4.myhuaweicloud.com/image-20220608214227727.png)

## 1.4. 定义异常类
1. **注意catch块排列顺序**：**不要将基类放在前面**，这样保证了**继承顺序(重要)**，顺序向下检查是否符合条件，一旦符合条件就不再向下查找了。

   在多继承时，**各个基类**都可以 catch 到这个异常对象

   **尽量用对象引用的方式来 catch**，避免拷贝 `catch(NonExists&)`
```c++
class FileErrors { };
class NonExist:public FileErrors { } ;
class WrongFormat:public FileErrors { } ;
class DiskSeekError:public FileErrors { };

int f(){
    try{
        WrongFormat wf;
        throw wf;
    }catch(NonExists&){...}
    catch(DiskSeekError&){...}
    catch(FileErrors){...}//最后一个可以接住，派生类向基类转换是允许的
}
int f(){
    try{
        WrongFormat wf;
        throw wf;
    }catch(FileErrors){...}//这样子底下都捕获不到，因为被基类捕获了，不会到下面去
    catch(NonExists&){...}
    catch(DiskSeekError&){...}
}
//Catch exceptions by reference
```

2. 实例:
```c++
class MyExceptionBase {};
class MyExceptionDerived: public MyExceptionBase { };
void f(MyExceptionBase& e) {
    throw e;//调用拷贝构造函数
}
int main() {
    MyExceptionDerived e;
    try {
        f(e);//传入的e是派生类型，在f中也是派生类型的，但是如果这个这个对象进行拷贝，那么会发生对象切片
    }catch(MyExceptionDerived& e) {
        cout << "MyExceptionDerived" << endl;
    }catch(MyExceptionBase& e) {
        cout << "MyExceptionBase" << endl;
    }
}
//输出:MyExceptionBase，为什么?调用了拷贝构造函数，拷贝构造的结果是MyExceptionBase类型的对象
//原因：Derived对象传入f，转成了父类的引用，但这个对象仍然是子类对象，在throw e时由于会调用拷贝构造函数，而调用父类还是子类的拷贝构造函数是编译时确定好了的，因此会调用父类的拷贝构造，所以发生对象切片。结果是父类的对象
```

## 1.5. 异常处理的特例
1. **无参数 throw**:将捕获到的异常对象重新抛掷出去`catch(int){throw;}`

2. **catch(...)**:默认异常处理,**这三个点是标准语法,捕获所有异常**

3. 系统调用的函数【*如析构函数和构造函数*】异常怎么处理？**必须在自己的函数内处理，不能抛出。**

   其中构造函数有点特殊，**初始化列表也有可能抛出异常**。因此要初始化表前，放置try-catch

   ```c++
   void f() 
   	try {
       	/*...*/ 
   	} 
   	catch (...) { 
   		/*...*/ 
   	}
   //等价于，即如果整个函数都是try，catch，没有之外的代码，则最外层的{}可以省略
   void f() {
   	try {
       	/*...*/ 
   	} 
   	catch (...) { 
   		/*...*/ 
   	}
   }
   //因此应用到构造函数
   class B{
   private:
       int i;
       double j;
   public:
       //放在初始化表的冒号的前面，注意左大括号在初始表后面
       B(int i, double j)
       try :i(i),j(j)
       {
   		...
       }
       catch (...){
   		...
       }
       //析构没有初始化表，和普通函数的一样即可
       ~B(){
           try{
               ...
           }
           catch(...){
               ...
           } 
       }
   };
   ```

4. 构造函数**参数的异常**怎么处理？这个就不属于构造函数自己处理了，而是**调用者来处理**

```c++
//异常可以用于对程序验证特征
template<class T, class E>
inline void Assert(T exp, E e)
{
    if (DEBUG)
        if (!exp) throw e;
}
```
5. 问题:如何应对多出口引发的处理碎片问题【*见下面的小动物例子*】，如果多个地方throw，则意味着这里有多个出口。
6. Java中在异常处理这一部分提供了Finally操作，无论在哪里没有抛出最后都会执行finally，因此可以在finally中进行delete处理
7. 可是C++中没有finally,那怎么进行处理呢?这个在C++中，可以使用智能指针【用一个栈上的智能指针包含我们要使用的指针，当离开智能指针的作用域时，自动析构】，**执行完异常处理后，必然执行析构函数**

```c++
//Know what functions C++ silently writes and calls
class Empty {}; 
class Empty {
    //以下是C++默认提供给空类的方法
    Empty();
    Empty(const Empty&);
    ~Empty();
    Empty& operator=(const Empty&);
    Empty *operator &();
    const Empty* operator &() const;
};
```

# 2. 使用析构函数来避免造成内存泄漏

## 2.1. 异常处理的例子:资源泄露【小动物收养保护中心】
1. 收养中心每天产生一个文件，包含当天的收养个案信息
2. 读取这个文件，为每个个案做适当的处理

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-C-plus-plus-advanced-programming/img/exception/2.png)

```c++
class ALA{//Adorable Little Animal
    public:
        virtual void processAdoption() = 0;
};
class Puppy: public ALA{
    public:
        virtual void processAdoption();
};
class Kitten: public ALA{
    public:
        virtual void processAdoption();
};
void processAdoptions(istream& dataSource){ 
    while (dataSource){
        ALA *pa = readALA(dataSource);
        try{
            pa->processAdoption();//处理可能会出现问题
        }catch (…){
            delete pa;// 在throw前也要delete pa，否则会throw后不能执行到后面的delete pa，造成内存泄漏
            throw;
        }
        delete pa;//正常执行也要进行处理，这就是多出口的问题
    }
}
```

- 结构破碎:被迫重复"清理码"2次delete的pa【多出口】(不符合集中式处理的想法、同时容易导致维护困难的问题)
- 集中处理？用智能指针【用一个**栈上**的智能指针包含我们要使用的指针，当离开智能指针的作用域时，自动析构】
- **RAII:将资源都封装成对象，资源获取时即为对象的初始化，资源的生命周期就是对象的生命周期**。这里对指针的处理就是如此

```c++
template <class T>
class auto_ptr{
    public:
        auto_ptr(T *p=0):ptr(p) {}
        ~auto_ptr() { delete ptr; }
        T* operator->()  const { return ptr;}
	    T& operator *()  const { return *ptr; }
    private:
        T*  ptr;
};
//结合智能指针使用
void processAdoptions(istream& dataSource){
    while (dataSource){
        auto_ptr<ALA> pa(readALA(dataSource));
        try{
        	pa->processAdoption();//只要对象结束，就会自动delete。无需自己在多个地方去写delete
        }catch(...){
            throw;
        }
    }
}
```

## 2.2. GUI应用软件中的某个显示信息的函数
1. handle class:句柄类【*句柄即引用/指针*】，就是处理智能指针==？下面的区别==
```c++
void displayInfo(const Information& info){  
    WINDOW_HANDLE w(createWindow());//针对windows窗体的一个指针，createWindow:返回一个窗体指针，WINDOW_HANDLE是别名
    display info in window corresponding to w;
    //delete w
    destroyWindows(w);
}
//专门的句柄类，处理窗体问题
class WindowHandle{
    public:
	    WindowHandle(WINDOW_HANDLE handler) : w(handler) {}
    	~WindowHandle() { destroyWindow(w);}//析构就会自动释放资源
        operator WINDOW_HANDLE() { return w; }//没有使用->重载，而是采用重载类型转换操作符，转换为WINDOW_HANDLE指针，将句柄类对象和包含的句柄一样的进行使用
    //和->没区别，效果一样，都能获取指针，也都能像指针一样操作，获取指针：T* get_ptr = auto_ptr.operator->(); T* get_ptr = (T)auto_ptr。
    private:
        WINDOW_HANDLE w;
        WindowHandle(const WindowHandle&);
        WindowHandle & operator = (const WindowHandle&);
};
void displayInfo(const Information& info){
    WindowHandle  w(createWindow())
    display info in window corresponding to w;
    // 无需delete
}
```

1. 第9、10课需要仔细听一下