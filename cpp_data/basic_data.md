# cpp复习笔记
==分为以下几部分==
1. C语言的初阶进阶部分
2. cpp的基础语法+类和对象部分(封装继承多态)
3. cpp内存管理以及stl的内存管理方式
4. cpp模板初级高级使用
5. stl实现与使用(mapset哈希)
6. 剩下一些庞杂部分 c++11 智能指针 类型转换 特殊类的设计+io流+异常处理

# 算法与数据结构概念
1. 数据结构 
  数组与链表 + 栈和队列 + 哈希表 + 二叉树红黑树 
2. 算法部分
  十大排序算法 + bfs/dfs各种搜索算法 + 贪心算法 + 动态规划 + 分治 + 回溯  + 二分查找...

## 1. c语言的初阶进阶部分
  1. static const 关键字作用
  swich case do while语句
  ifndef语句的作用
  
  2. ==面试题== 不创建第三个变量进行ab元素交换 + ^ 这个符号&& || 符号的运算顺序 从左边到右边 
  
  3. 数组sizeof + 逗号表达式 + 条件操作符
  隐式类型转换-》整型提升 char变成int等 + 意义 cpu运算器一般以int进行计算，所以需要转换
  
  4. 指针的作用：存放对应类型的首地址，决定解引用如何去使用，决定解引用后能访问多少个字节以及+1-1偏移几个字节。
  指针数组 数组指针其实就是一个指针 指向数组的首地址
  ```cpp
  int* arr3[5];  //指针数组 
  int (*p2)[10]; //数组指针
  ```
```cpp
    int my_strlen(char *s)//指针求长度
{
       char *p = s;
       while(*p != '\0' )
              p++;
       return p-s;
}
```
  
  5. 整形和浮点底层存储方式 + 原码+反码+补码 + 大端小端的产生与判断-》使用大小端的场景
  无符号数 直接存 + 有符号数存补码
  使用补码，可以将符号位和数值域统一处理； 同时，加法和减法也可以统一处理（CPU只有加法器）
  浮点数的存储-》符号位 + 指数8/11 + 小数位
  
  5. 回调函数 -》指针 仿函数 等实现-》个人理解将函数以参数的形式进行传递 -》实现函数调用间的解耦
  
  6. kmp算法 字符串比较大小复制扩容等实现了解 -》其实就是使用指针按字节进行拷贝
  
  7. 结构体内存对齐 + 位段节省空间 + 枚举和联合
  
  8. c语言动态内存管理 mallco free/calloc(num,size)0 realloc(*ptr,size)扩容 + 柔性数组
  
  9. c/cpp程序地址空间 堆向上 栈向下原因 + mmu的作用-》其实就是mmu没产生出来之前就确定的， 现在mmu出来之后没必要改动了， 当时为了减少内存碎片的出现

  10. coredump文件的使用 -》打开关闭产生coredump
    头文件中的ifndef/define/endif是干什么用的？
  
  ## cpp基础&面向对象特性
  ### 基础语法
  1. 函数重载和预处理编译汇编底层实现
  2. 引用和指针的底层 + 使用的注意事项 auto* auto&

  ### 类和对象封装继承多态
  1. 访问限定符 -》编译 数据映射内存-》默认的访问限定符
  2. 类的对象模型的存储以及计算
  
  3. this指针是什么 存在哪里

  4. 类的六个默认成员函数 
    构造析构拷贝构造赋值运算符重载取地址重载
    拷贝构造传引用
  5. 深浅拷贝

  6. const + static 修饰不同的变量函数的作用
      最小权限原则 编译器处理const 静态 共享 不存在this 

  7. 初始化列表初始化-》must ->引用类型+自定义类型+const类型
     声明顺序为初始化顺序
  8. explicit 防止构造函数返回出来的类被隐式类型转化

  9. 友元 类和函数 -》访问类的私有成员-》破坏封装
      内部类外部类-》sizeof外部类
      
### 内存管理和stl的内存管理
  1. cpp内存分布 —》 内核空间 栈共享区堆 数据段代码段

  2. new delete operator new/delete [] 定位new
  
  3.  内存泄漏分类-》堆系统资源  解决方式

  4. stl 128字节分为大内存和小内存 
    大于128为一级 malloc free 
    失败判断有无可以释放的内存 不行就抛异常
    小于128为二级 free list+内存池
    https://blog.csdn.net/qq_26822029/article/details/82915529
  
  ### cpp模板初级高级使用
  1. 泛型编程 类模板 函数模板
  编译阶段编译器进行特殊处理
  模板的实例化 -》显式和隐式
  2. 模板特化
  3. 分离编译
  4. 类型萃取
  
  ### STL部分
  1. 六大组件
  容器 string vector map
  仿函数 less greater 
  空间配置器 allcator 也是一种内存管理手段 类比智能指针
  算法 find swap reverse sort merge
  配接器 stack queue priority_queue
  迭代器 iterator 
  
  通用内置函数
  resize reserve 区别与联系
  resize会改变cap和size的大小 
  reserve只改变cap不改变size 因为仅仅是预留不初始化 因此也不能访问到size之外

  2. string 
  a. 对string的实现进行回顾
  b. string的深浅拷贝写时拷贝实现方式 优缺点比较
  ==c. 引用计数和static的区别==
      引用计数多开辟四个字节 -》当进行下标访问或者更改时候，进行拷贝新的返回新的str的元素 旧的引用计数减一 新的加一

  ==string迭代器 iterator其实是一个 char* 的类型==


```cpp
    typedef char* iterator;
    //比如迭代器
    iterator begin() {return _str;}
    iterator end(){return _str + _size;}

```

3. vecotr 
  a. vector的迭代器失效问题 扩容问题(sgi的版本和其他的版本不同导致 vs和g++不同)
       resize、reserve、insert、assign、 push_back等 引起迭代器失效
       解决 使用前重新赋值

  b. 实现复习 自己实现的vector进行拷贝的时候也需要注意 涉及自定义类型的拷贝需要注意深浅拷贝 以及内存泄露

  c. stl实现的是深拷贝 也就是去访问了内存地址 然后进行拷贝

```cpp
    template<class T>
	class vector{
  public:
    typedef T* iterator; // 对模板进行重命名
    typedef const T* const_iterator;

    vector() //初始化列表 初始化迭代器指针
      :_start(nullptr)
      ,_finish(nullptr)
      ,_endofstorage(nullptr)
    {}

```

  4. list
    1. 实现方式listnode + iteratornode + list -> 封装节点 迭代器实现指针功能 最终的类
    2. 迭代器失效原因
    3. 迭代器与原生态指针迭代器的区别
    4. list与vector的对比
    
  5. 容器适配器 stack and queue  and priority_queue (堆) 默认大根堆 
      stack queue 底层默认是deque 因为需要尾删头删 扩容等机制
      priority_queue 底层默认是vector 因为需要根据下标计算 只有在同一个下标中进行计算才有意义

  6. deque 
    1. 底层实现了解 中控器 + 碎片空间 + 不适合遍历
    当前连续空间的首地址 + 当前连续空间的末尾地址 当前遍历位置 以及map中当前的地址

    ```cpp
      template<class T,...>
      struct __deque_iterator{
        ...
        T* cur;
        T* first;
        T* last;
        map_pointer node;//map_pointer 等价于 T**
      }
```




































