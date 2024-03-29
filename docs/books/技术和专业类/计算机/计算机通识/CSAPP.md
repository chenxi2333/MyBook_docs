# Chapter1 计算机系统漫游

# Chapter2 信息的表示和处理

1. 基于二进制的表示的计算机系统。

   1. 不同位数、不同架构的系统中C语言的中类型是由不同的长度的，比如long在32位系统里4字节，在64位系统中8字节。

   2. 16进制的意义是能够做到“4个2进制”直接组合，便于书写 观察。

   3. 位数的含义是地址的位数。

   4. 选择二进制的重要原因就是bool运算。

      1. 按位操作是C语很重要的功能。单个的| & ~ ^(或、与、非、异或运算符号)
         1. &又被称为mask，因为可以便捷的做到“遮掩”，留下遮掩运算中1的位。
      2. 注意与|| && !的区分，双符号是数值本身的真假判断，只有0是False，返回只有0和1。
      3. 按位运算——左移和右移。
         1. Log<<和>>:多出来的位会填充0。
         2. Arith.>>和.<<：多出来的位会以原来的最高位填充。
         3. 大于等于字长、或者小于0的移动通常被判定为非法。
   
   5. 二进制数字和不同数据类型的转换方法：
   
      1. 无符号数可以直接幂求和。有符号数采用了补码编码。
   
      2. 有符号数可以看作是最高一位的幂运算取负数，其它位数全部求和。其实也很好理解——如果第一位是1，那么就从负数开始计数，加上后面位数的数值；如果第一位是0，就从0开始正常计数——这个第一位被称为是符号位。
   
         1. 因此符号数的0不是正负的“连接处”。全部1，则可以得到-1。
   
         2. 如果让人去判断：第一个数判断正负，如果是1，负数，后面的数取反+1后就是这个负数的绝对值。由于0只有一个，并且算在了“正数”中，因此负数会比正数“多一个”。
   
         3. 有符号数（Two's Complement）和无符号(Unsigned)数的转换：可以转化成二进制然后再转化。
   
            1. T2U：如果第一位是1就直接加上最高一位的2次幂2^W，如果是0则不用改变。
            2. TMAX*2+1=UMAX
   
         4. C语言是少数能够明确的使用“unsigned”的语言。
   
            1. C语言能够在unsigned和signed之间隐式转换，如果两者中有一个无符号，那么会把另外一个自动转化成为无符号数。在数字后面加一个u，说明这是一个无符号数。
   
            2. (int)(unsigned)属于更高的强制类型转化，可以把一个数做类型转换。
   
               > -1>0U ; 2147483647U< -2147483647-1，这两者都是因为自动把负数转化成了无符号数进行的比较。
               >
               > 2147483647 > (int)2147483648U，两个有符号数，后者自动转化成了-1。
               >
               > (unsigned)-1> -2 ,两者自动转化成了无符号数，相当于是4,294,967,294>4,294,967,293
   
            3. > for(i=n-1;i>=0;i--)这句话中如果i是unsigned，那么循环将会永远进行下去——因此i到零之后继续-会得到UMAX，如果循环中使用到了数组索引，则会报超出数组上限的错误。当然，如果使用的是有符号数，就不会出现这个错误。 
   
   
   > 有符号数另外两种表示方法是反码（负数从零开始）和原码（符号位仅仅表示符号）,这两种方式中都存在-0这个数[10000...]
   
   1. 拓展Extension：一个数拓展位数的时候怎么改变
      1. 无符号数：zero extension
      2. 补码：符号拓展sign extension
         1. 第一位取出，放到最开始，其他位数补0。0的话到此就可以了
         2. 如果是负数，首位为1，那拓展出来的位数补1。
         3. 总结，把第一位复制k份，补充到拓展的位数上。
      3. 在C语言的拓展操作上，长度和符号的转换一般先进性符号和无符号之间的转换，再进行字长的拓展。 
   2. 截断Truncating：符号数的位数缩短会发生什么？无论是哪一种数，截断都是直接丢弃最高的位，因此很容易改变值。
   
      1. unsigned直接弃最高位。相当于是原来的值对截断的最低位2^k进行的一次“取模运算”。很容易理解，取模运算就是“不超过这个数字的部分”。
      2. signed：补码截断可以先转化为无符号数，取模，然后再转化为符号数。

### 整数运算

1. 无符号数加法：直接相加，进位，超出之后将会溢出。溢出后得到的结果就是结果对最大数$2^w$取模后的结果。
   1. C语言对无符号数的溢出不会有提示，但可以检测是否溢出。
      1. 基本思路：因为无符号数大于0，相加的结果一定是高于原本的数值的，如果溢出，则一定会小于原先的数值。
2. 补码相加：补码的特性让它的加法可以做到直接相加，需要注意的只有溢出的情况将会导致符号的错误。
   1. 补码计算中的溢出的符号位有时候可能只是正常的符号转换。只要结果能够在范围内，就不会出现计算错误。
   2.  溢出只发生在结果超过TMAX和TMIN的情况下。
   2.  可以观察结果的符号是否出现了颠倒——如两个负数加出正数或者相反的情况，则说明溢出了。只要符号正确，都代表了结果是正常的。这也是用来检测溢出的一般方法。
3. 乘法：同样会遇到溢出。
   1. 无符号数乘法：超过上限则进行取模运算。
   2. 有符号数：相乘后同样使用截断。可以把结果转化成无符号数，截断后再转化成为有符号数。
   2. 位级等价性：**同样的编码，无论是补码还是无符号数，即使相乘之后，完整的（2w位的位级表示）结果不同，但是经过截断后的结果编码（位级表示）永远是一样的。**
4. 一般来说计算机乘以2的幂会使用左移。
   1. 这一点对于有符号数和无符号数都适用。 只要一个有符号数乘法过后不会溢出，那么左移运算是能够保证正确性的。
   2. 能用位移做运算对于编译器是最快速的——是需要一个时钟周期。因此一般来说，编译器为了效率会尽量使用这种乘法组合来代替普通的相乘。
   3. 乘法的方法在二进制模式下同样适用，因此一个乘数K分解为二进制之后就可以使用左移和加法去完成计算——可以使用的有两种形式，本质其实就是一个等比数列求和。当然选择“位移+加法”还是乘法对于不同的机器之间有不同的衡量，需要权衡。
   4. 补码的乘法结合需要从本质上去考虑，因此最高位的相加应该对应更改为相减。
5. 同理，对2的幂进行除法可以右移。
   1. 算数右移可以用1填充空余位，可以用来计算补码的负数除法。
      1. Java中的右移当作是算数右移
      2. 结果是向下舍入，在原数的k位加上一个偏置1后，对这个数进行右移k就可以实现向上舍入。
         1. 为了实现向零舍入，需要对原数进行判断。
6. 乘法和除法不要太过于拘泥于公式。
7. 一个数字取反数的计算方法：
   1. 补码按位取反然后+1；unsigned=2^w-x(x!=0) 。
   2. Tmin的取反+1将会得到的数由于溢出，因此只能够得到它本身，即TMIN。——因此-x==x是可能存在的情况
8. 递减：对于Unsigned，0-1->UMax。



### 机器字长

1. 储存上区分：大端序、小端序（常用）。小端序它的字节（8bit）是倒过来排的。
2. 因为char只有8位，因此顺序永远是对的。
2. malloc参数值类型是size_t，因此无法申请一块高于size_t位，即（2^32）字节以上内存大小。



### Floating Point浮点数

1. 如何使用二进制表示小数：顶点表示法——小数点右侧表示2^(-x)。
   1. 不能表示很大的数字，并且计算机中也不好储存，不够灵活等缺点
   2. 十进制的小数和二进制的小数之间有时候并不能够完美的转化。
2. IEEE浮点表示：符号位s+阶码exp+尾数significant(frac)
   1. 其中：符号决定正负，阶码决定最小分数，位数决定数值。，具体的计算公式为 $v=(-1)^sM2^E $
   2. 不同位数的机器上有不同的表示方法：
      1. 32bits:1+8+23
      2. 64bits:1+11+52
      3. 可以说frac的位数决定了数据的有效位数，位阶则决定了这些有效位数的“位阶”——当然，需要注意这些都是在二进制下讨论的。
   3. 为了扩大IEEE浮点数的表示范围和灵活性，存在四种表示数值的方法(主要以阶码exp作区分)：
      1. Standard规格化表示：阶码不全1或者0
         1. E=e-Bias,Bias=2\^(k-1)-1（k为位阶的位数）。位阶的范围在\-2\^(k-1)-2~2\^(k-1)-1(因为没有全零和全1的状态)
         2. M=1+frac,隐含为1开头的定义方式。frac部分表示的是“小数点”后的二进制数。
      2. 非规格化：阶码全0
         1. E=1-Bias,Bias=2^(k-1)-1（k为位阶的位数）
         2. M=frac,隐含为1开头的定义方式。
         3. 最大的非规格数和最小的规格数相差2^(1-Bias)。
      3. 无穷大：阶码全1，尾数全0
      4. NaN（Not a Number）：阶码全1，尾数非0
   4. 这种计数法可以让数据密集程度：越靠近0数据越稠密。

3. round舍入：向上舍入、向下舍入、向零舍入、向偶数舍入
   1. 中间值向下舍入。
   2. 向偶数舍入：中间值优先向偶数舍入，其它的不变。
4. 浮点数的运算
   1. 浮点数的运算中编译器将会自动舍入，编译器只能够保证一个合理但不是很精确的结果。
   2. 浮点的加法不具备结合律，由于编译器处理加法的过程中会因为处理舍入的位数，因此最后的结果上将会存在差别。
5. C语言的浮点数：
   1. float和double，使用了偶数舍入。式子中自动转化成浮点数进行运算。
   2. int到double的互相变化，可以完全转化，整数部分能够完全放得下。但是到float就会舍去部分的数。
   3. 整数转化成浮点数，整数的数值对应了浮点数的最高有效位数。





# Chapter 3 程序的机器级表示

## 历史

1. Intel处理器俗称为x86，从最早的8086到如今的Core i9进行了不断的进化升级。
2. CPU的进化是符合摩尔定律的。
3. 如今如ADM这样的公司也开始在技术上追赶上了Intel。

## 程序编码

1. 在UNIX中可以使用GCC编译器对c源代码进行编译生成目标代码文件。
2. 机器级代码：指令集和指令集架构ISA。现代比较通用的ISA有x86-64以及ARM。
   1. 对于机器代码而言，内存中只有相同的数据，从哪里取，怎么使用都是未知的。
   2. 机器语言提供的操作也是底层的、基础的。
3. gcc可以后面添加-s命令就可以输出汇编文件。目标文件是二进制的格式，无法查看，它所对应的汇编指令和-s生成的文件是对应的。
   1. 反汇编器：`objdump -d 目标代码` 可以从目标代码的二进制文件中还原编译语言。
   2. gcc提供的汇编语言很难理解，因为它包含了太多的伪指令以及未加注释说明的内存位置。
   3. 汇编语言能够插入在C语言中。
4. 数据格式Intel中“字”（不是字节byte）是16位。
5. 访问信息：寄存器x86中包含了一组16个64位寄存器。
   1. 寄存器中的低8，16，32，64位都可以通过字节操作单独访问。
   2. 不同的寄存器有时候带有一些专门的功能，比如rbp是栈指针。
   3. 操作数指示符：如何访问寄存器以及内存——不同的寻址方法。
      1. 通常是寄存器中储存内存地址，然后访问内存中对应的地址里的数据。
   4. 数据传送指令：MOV类，对于不同长度的数据有衍生出的几种指令。
      1. 效果很简单，就是把数据从一个位置复制到另外一个位置。第一个操作数是源，第一个操作数是目标位置。
      2. 不过存在限制：不能够两个位置都是内存，至少存在一个寄存器。寄存器部分的大小和mov最后的字符所指代的长度相匹配。
      3. MOVS类指令可以扩充填充到目的寄存器。
      3. MOVZ类：是不同长度的字之间传输的指令，做了零拓展（填充零）
      3. MOVS类：符号拓展（填充符号位）
   5. 压入和弹出栈数据
      1. pushq：两步操作，栈顶指针减8，然后将值写入新的栈顶地址。
         1. 栈一般“倒过来画”，实际上内存中栈底指针是在高位。

### 算术和逻辑操作

1. 算术和逻辑操作
   1. 加载有效地址：作用是从内存读取到寄存器。leaq
      1. 这个命令可以做快速简单的运算。
      2. ​                                                                                                                                                                                                                                                            
   2. 一元和二元操作：
      1. 只有一个操作数的计算就是一元操作，比如++这种就是一元操作。
   3. 移位操作
      1. 逻辑异或可以这么用：xorq %rdx,%rdx可以把rdx设置为0。
      2. 
   4. 特殊的算术操作

### 控制

之前所讨论的都是直线执行的代码，汇编语言中全部的跳转都是依靠JMP类实现的。jmp分为条件跳转和非条件跳转。

cmp指令可以改变几个标志位的值，test、条件跳转这样的命令则可以根据标志位的值执行。

>  JMP最为自由，因此才会需要各种if或者while这样的封装，来限制它的自由跳转的同时保留功能。

#### 如何把if转换为jmp？

1. 用条件控制来实现条件分支：conditional jump
   1. 首先转化为“goto”，再进一步转换成jmp
2. 用条件传送来实现条件分支：conditional move
   1. 这种做法的好处在于能够减少分支带来的流水线暂停。
   2. 坏处就是这种方法作用范围是有限的。

#### 如何把while和for改写为jmp？

1. do..while
2. while
   1. 跳转到中间/guarded-do使用条件分支

#### 如何把switch转化为jmp

1. 使用的是跳转表格的方法。
2. 其实并不能够准确的判断switch(x)中的x，默认情况下之用的是0~n，正好对应了一个表。



## 过程 Procedures

过程是以中国很重要的抽象方法：所谓的过程就是函数调用中是如何完成——传入参数，返回值这两个过程的。

过程P调用过程Q，包含了以下必须具备的机制：传递控制（指令执行循序上的跳转）、传递数据（传参和返回）、分配和释放内存。

1. Stack运行时栈结构：内存管理中先进后出的栈结构很适合。
   1. Stack栈在内存中并不特殊，它是专门用来被储存程序的信息的地方。
      1. 栈的储存顺序是反的。栈底的地址高。rsp指向栈顶元素。
      2. 使用push和pop对地址进行操作。
   2. Stack-Frame：栈帧
      1. 过程需要的储存空间超出了寄存器能够存放的大小时候，就需要在这里分配空间。
2. 转移控制——call Label ：调用指令。
   1. 栈指针操作，把返回地址压入栈，然后跳转到调用地址的第一条指令。
   2. 直到遇到ret指令，就从栈中弹出地址，返回后继续执行。
   2. 栈的结构很适合调用——保存状态，返回值。
   3. 通过寄存器来传递参数——返回值保存在%rax。传入参数保存在六个特定的内存中。
3. 数据传送：x86中，大部分的参数传送是寄存器实现的。
   1. 参数的**值**首先被复制进入特定的寄存器，返回值同样保存到特定的寄存器。
4. 栈上的局部存储
   1. 如果传递的参数寄存器无法保存，就需要局部存储。
5. 寄存器中的局部存储空间
   1. 寄存器组是唯一被所有进程共享的资源，当新的进程被调用时候，旧的进程保存在寄存器的值要么不动，要么会将它们压入栈中。在进入栈帧中时也会记录他们保存的寄存器。%r12~%r15都是需要被压入栈保存的寄存器。
6. 递归过程：
   1. 递归调用自身，每一次调用都会分配独立的资源，多个递归之间不会互相影响。
