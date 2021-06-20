# 08 Variables in C++

在C++中，不同的变量类型之间的唯一区别就是大小，占用多少内存！

float a = 5.5;会被优化成double，如果不想：float a = 5.5f；

bool类型只需要占用1bit，但是内存在寻址时无法寻址到bit，只能寻址到bytes；所以bool还是占用了1bytes；

但是你可以巧妙的将8个bool存在一个byte里面；

sizeof（）查看大小；

# 09 Function in C++

函数的主要目的：防止代码重复；

当调用一个函数时，需要为此函数创建一个stack frame（栈框架），同时将参数之类和返回地址push到栈上，然后跳到程序的某部分，执行函数里的指令，然后push返回值；返回给函数之前调用的地方；

# 10 C++ Header Files

头文件：函数声明，以供多个cpp使用；告诉当前cpp，函数是存在的；

#pragma once ： 只include一次，防止把单个头文件多次include到一个翻译单元里；header guard（头文件保护符）

```c++
#ifndef _LOG_H_ //作用与上述相同
#define _LOG_H_
#endif
```

“”会在优先在当前路径搜索头文件

<>不会优先在当前路径搜索头文件

# 14 Loops in C++ （for loops，while loops）

for循环

while循环

do while()

# 15 Control flow in C++ (continue,break,return)

continue：直接进行下一次的迭代；

break：直接跳出循环；

return:  直接退出函数；

逻辑程序的本质：14 + 15；

# 16  POINTERS in C++

原始指针（raw pointer）not 智能指针（smart pointer）

指针：一个整数，这个整数就是某块内存的地址；

pointer is just an address ，it ,s just an integer which holds an address in memory;

指针的类型是我们在告诉编译器，当我们进行读写的时候，使用什么类型去操纵这块内粗；

申请在heap上的内存

```c++
char* buffer = new char[8];
memset(buffer, 0, 8);
delete[] buffer;
```

二级指针:一个整数，这个整数就是某块内存的地址，但这个地址索引的内存上仍然存储着一个地址；

# 17 REFERNCAS in C++

最终来看引用就是指针；

引用只是基于指针的一种语法糖（syntax sugar）；









