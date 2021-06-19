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

# 



