# C++入门笔记



# Essential C++

## Chapter 1 编程基础

1. 基础数据类型

   * 类，class让用户自定义数据类型，C++中事先定义了一些基础数据类型。

   class机制，让我们能够增加程序内的抽象化层次。

   class一般再头文件中声明operation，再代码文件中包含实现内容。

   * 对象的初始化：class<template> + name，可以赋予初值；
     * 另外一种方法是用的“构造函数法”——是用于给那些更加复杂的class赋予初始值的方法。

2. 运算符号

   * C++中的>>和<<有点类似于Linux中的“文件流”的意思
   * cout代表了输出端口，cin代表了输入的端口（缓冲区），cerr代表了Error的输出。

3. 条件分支和循环控制语句

4. 复合类型，字符串和向量

   * C++中同样支持指针，也有*（提领）和&（取址）操作
   * 数组和指针的用法和C中间基本一致
   * 除此之外，C++标准库提供了vector类来定义容器。`vector<class> pell_seq(seq_size);`
   * 两者的用法基本类似，但是vector不支持初始化列表的定义方式，但是可以通过语句`vector<int> seq(elem_vlas,elem_vals+seq_size)`利用数组开头和结尾的位置来初始化vector。
   * vector的好处就在于可以调用方法来获得这个数组的信息

5. 文件的读写

   * 定义了一个ofstream的类型，可以用来（输出）操作文件，返回值是成功。写入文件使用<<，将输出信息定位到这个文件；
   * ifstream可以输入操作文件，用的符号是>>(从文件流向变量)，infile是一个“自动迭代”指向下一个的类型；

## 面向过程的编程风格

 以函数为主要的手法。

当我们调用一个函数的时候，会在内存中建立一块特殊区域，称为“程序堆栈”，随着函数的完成被释放，形式参数是在这个区域中进行操作的。如果要返回堆栈中的临时地址，会报错，只能把它作为值传回原来的位置。

C++中的动态内存管理通过new和delete来实现。

```c++
int *pi;
pi = new int;
pi = new int(1024);//直接为对象赋予初值
delete pi;
delete [] pi;
```

传入的是可以是pointer和reference，通过这两种方式的参数传递可以实际改变参数。

**reference是C++独有的语言特性**

C++中可以定义reference的数据类型，代表了一个“快捷方式”，对它的操作等同于直接在原数据的地址处进行操作。

```c++
int i = 0;
int & iRef = i;
int * pRef = &i;
//等效于(*pRef) 
(*pRef)++;//等效
iRef++;  // i = iRef = 1
```

* C++允许在函数定义时候为函数提供默认的值。
* 局部静态对象：即在函数中用static前缀，每次调用时候会保留上次的数值。
* 声明inline函数：在一个函数前加入inline的前缀，此函数就是inline，有点类似于C中间的“宏定义函数”，本质上是替换。好处是不需要反复创造额外的堆栈空间，适合于体积小而且经常被调用的函数
* C++提供了重载函数，编译器能够自动选择适合填入参数的函数。
* 定义模板函数：function template，就像vector<template>一样，能够灵活变动函数类型。
* 函数指针：可以做一个“函数组”
* 设定头文件：在头文件中对函数进行声明





# C++语言学导论

# C++程序设计语言

## Chapter17 构造、清理、拷贝和移动

### 构造和析构函数

1. 构造函数用来在类初始化的时候调用，析构函数在类被销毁（包括例如退出作用域时候的自动销毁，以及手动销毁的时候）时候调用。
   1. 析构函数就是在构造函数之前加~
   2. 构造函数不会有返回值，或者说可以把返回值看作是类本身？



