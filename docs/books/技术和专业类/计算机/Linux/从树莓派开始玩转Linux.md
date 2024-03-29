# 从树莓派开始玩转Linux

## Part3 Linux

1. Linux 所有应用层面的都以“进程”位单位。进程是程序的一个具体实现，是是执行程序的过程。在Linux可以使用ps查看。

   一个程序可以执行多次从而产生多个进程，操作系统一个重要的功能就是进程管理。

2. Linux把所有读写数据的对象都当作文件，所以Linux有“Everything is a file”的说法。甚至设备也是以文件储存，计算机通过文件和设备进行沟通操作。数据在文件之中流动，称为“文本流”，文本流有序完整的传输，实现了计算机模块之间的通讯链接。
   1. 每个**进程**，自动打开三个流的端口——Standard Input/Output/Error。例如bash程序的输入连接到键盘，输出打印在屏幕。
   2. 重定向>>：把某个进程的输出可以导向另外一个文件，让流动的数据走向特定额方向。
   3.  < 可以改变输入的来源：让输入来自某个文件而不是键盘。
   4. 管道|：pipe变更文本流的方向，但是目的是另外一个进程。借用管道，可以把进程的输出导入另外一个进程的输入上去。
      1. 通过管道，可以把功能互相连接，组件复杂的程序。
   5. 文件的相关命令：cat\head\tail\diff等都是输出文件的方法

3. Linux权限管理：用户、组、id、root
   1. 用户信息文件：/etc/passwd中，储存了用户的信息。
   2. 文件的权限以及管理

4. bash：bash 是一个命令解释器，它是可以编程的。
   1. 变量的定义和调用：echo显示变量，$表示变量，可以在\$之后使用表达式和常量值。

   2. ehco $?可以获得上一句命令的返回码。

   3. 命令行中可以使用&&和||运算，前者表示前一个指令成功则执行后一条；后者则表示第一个指令失败了则执行第二条。

   4. bash脚本：多行的bash命令写入一个文件，在这个文件执行的时候就形成了所谓的bash脚本。第一行#!/bin/bash开启，说明本文档是bash脚本。

   5. 函数：可以在脚本中包含函数，函数可以包含参数，可以在脚本外调用。

   6. 跨脚本调用：source命令可以实现跨脚本的调用

   7. 逻辑判断：test命令，可以检查文件的存在、是否可读，也可以比较参数的大小。

      1. 可以使用与或非进行逻辑组合运算
      2. 要注意真返回0，假才会返回1

   8. 选择结构

      ```bash
      if [condition]
      then
      	xxx
      else
      	xxx
      fi
      ```

   9. 循环结构

       ```bash
       while []	
       do
        xx
       done
       
       for xx in XX
       do
        xx
       done
       ```

   10. bash语言不是真正的编程语言，它是一种面向过程的编程方法，本质上是一个解释程序，是对底层封装后的产物，虽然比不上C语言这样的高级语言，但是在系统中却更加方便与快捷。

### Linux 的完整架构

1. linux系统可以分为内核和应用程序两个部分，内核负责的是计算机资源的调配使用，与底层的硬件直接相关。而应用程序则会通过与内核之间的接口调用来实现特定的功能。
   1. 内核的活动称为内核模式Kernel Mode，应用程序的活动称为用户模式User Mode
      1. 对于用户而言，系统提供的调用就是最小的功能单位。
   2. 内核可以调用的有两百多种，比如文件的读写、进程的检测等等。
      1. C语言中的库中包含了这些接口的封装——很多都是使用了宏定义的方法去做的。stdio这样的标准库已经是系统库上再一次封装后的结果了。
      2. man 3 库函数 可以查看库函数的帮助文档。
   3. Shell是一个特殊的应用程序，它的功能就是把底层的功能用简单的接口呈现给用户。
      1. Shell让用户不需要经过编程以及编译这些过程就可以调用底层的功能。
      2. 其它应用程序（可执行文件）也可以借助Shell来直接执行。
2. 函数调用和进程空间
   1. 应用程序的进程会获得独立的内存空间，这个空间就是进程空间。
   2. C语言中的函数对应的底层汇编语言中的跳转和块。
   3. 栈与情景切换：
      1. 栈是为了配合函数调用而产生的。总是最下级的函数处于激活状态，等待函数完成之后栈会弹出这个最下层的进程。
   4. 本地变量
   5. 全局变量和堆
      1. 堆（Heap）用于存放动态变量（Dynamic Variable）
3. 信号：进程之间的互相通讯
   1. 按键信号传入shell，Shell会进入阻塞等待命令阻塞结束。每个Shell最多有1个前台进程，这个进程会阻塞。按键信号不会传入后台。
   2. kill可以对进程发出各种信号（先使用ps命令找到进程号）。
   3. 信号机制让系统能够和进程进行沟通。
      1. 信号从系统到进程，进程总是在特定的时机下才被查看。然后被处理。
      2. 信号只是一个整数，并不具备很多的信息量，通常涉及额问题都是系统运行的关键问题，比如通知进程终止、恢复等等。

   4. 信号处理：信号与其说是“命令”不如说是“通知”，面对信号，进程可以选择无视或者按照自定义或默认的方式去执行操作。
   5. C语言中的信号处理在头文件signal.h中，可以在程序中调用使用。




## Part4 深入Linux

本部分将会介绍Linux的高级概念，以及内核的主要功能。

### 进程的生死

- 进程从Init开始，在运行期间创建的进程都是fork出来的。所谓的fork，就是从父进程中建立一个子进程的分支。
  - PID是自己的进程，PPID则是自己的父进程。
- fork系统会在建立的过程中返回两次，分别把子进程的PID返回给父进程，以及把0返回给字进程，让它知道自己是子进程。
- 资源的fork：
  - 原有的进程空间、进程描述符复制到新的进程空间。
- 最小权原则：进程可以在运行过程中变换权限。
- 进程的终结：进程一般可以自发的终结，某个进程终结时，父进程会获得通知，删除进程对应的内核信息重任，落在了父进程上。
  - 父进程早于子进程终结，子进程就会和进程失联，称为孤儿进程Orphand Process。孤儿进程一般交给Init托管，如果没有wait，这个进程会变成Zombie进程。



### 进程之间的通讯（资源共享IPC，Inter-process Communication）

1. 管道：进程之间可以通过文件、信号来交换信息，不过最常用的方法还是使用管道来连接进程的输入和输出。
2. 管道的创建同样也是fork的机制，正如其名，管道会根据两个文件的输入和输出端口建立一个同时接上两边的通道。
   1. 不过上述这种只能用于父子进程之间，因而Linux提供的命名管道，创建了一个FIFO文件，连接两个进程——借用文件系统的创建、搜索和删除功能，命名管道在管理上更加方 便。
3. 其它的资源共享方式：
   1. 消息队列：队列的方式来处理数据
   2. 共享内存
   3. socket套接字：互联网上常用的一种方法



### 多任务与同步

Linux支持并发，就是说可以同时执行多个任务。

单核CPU虽然不能够指令上实现真正的并发，但是可以通过分时来实现同时多个进程。

1. 多线程：不同于多进程并行，多线程是对于进程而言的，有单线程进程和多线程进程（Multi-Threading）之分。
   1. 多线程编程中，需要在进程空间中用到多个栈来保存任务切换时候的状态和数据。
2. 竞态条件：并发容易产生RaceCondition，数据共享的时候由于同时操作某个数据造成的错误。
3. 多线程同步：同步Synchronization，是指在一定的时间内只允许某一个任务访问某一个资源。是一种解决竞态的方法。常用的方法有：
   1. 互斥锁：一个定义的特殊变量，只允许同时有一个线程操作变量。另外一个必须等待互斥锁打开后才能使用变量
   2. 条件变量：保存为全局变量，一般和互斥锁配合使用，在这个变量达成某种条件的时候去操作互斥锁，让线程等待。
   3. 读写锁：包含了R和W两把读和写的锁，R锁可以被多个线程同时获得，但是W所只有一个线程能够获得。

### 进程调度

进程是一个虚拟抽象出的概念，管理进程，并给进程分配计算机的资源，是操作系统中调度器Scheduler的任务。

1. 进程的状态最基本的就是三种：Ready、Running、Block。
   1. 阻塞就是让出CPU，可以主动也可以交给调度器来强迫阻塞。调度器的主要工作就是选择Ready的程序给CPU，另一个就是让一些执行中的进程阻塞。
2. 进程分配CPU的基本依据，就是“优先级”。
   1. Linux中分为普通进程和实时进程，后者优先级最高，只能通过Linux系统创造而不能被普通用户创造。
   2. 普通用户的优先级可以设置变量，越小优先级越高。
3. O(n)和O(1)调度器：
   1. Linux在优先级调度策略之上还需要继续优化，充分发挥多任务系统的优势，通过把时间分成大量的微笑时间片Epoch，时间片开始的时候找到Ready状态的最高优先级的进程，最早直接遍历，后来会先拍好优先级然后选择，复杂度从n下降到1，调度器也由此得名。
   2. O1调度器会用两个队列分别存放活跃的和过期的（已经用过切片）进程。
   3. CPU还会根据平均等待时间调整顺序，来给用户更好的体验。
4. CFS完全公平调度，自2007年起完全取代了上述方法，它采用了一个VirtualRuntime记录执行时间，调度器将会选择虚拟运行时间最少的进程。

### 内存的一页故事









