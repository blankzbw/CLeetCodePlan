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

```c++
#include <iostream>
int main()
{
	int a = 5;
	int& ref = a;
	ref = 2;
	std::cout << a << std::endl;
	std::cout << &a << std::endl;
	std::cout << ref << std::endl;
	std::cout << &ref << std::endl;
	//std::cout << *ref << std::endl; // error
	return 0;
}
console：
2
004FF8A0
2
004FF8A0

```

引用：顾名思义是某一个变量或对象的别名，对引用的操作与对其所绑定的变量或对象的操作完全等价；

https://www.cnblogs.com/duwenxing/p/7421100.html

1.&不是求地址运算符，而是起标志作用

2.引用的类型必须和其所绑定的变量的类型相同

3.声明引用的同时**必须对其初始化**，否则系统会报错

4.引用相当于变量或对象的别名，因此**不能再将已有的引用名作为其他变量或对象的名字或别名**

5.引用不是定义一个新的变量或对象，因此**内存不会为引用开辟新的空间存储这个引用**

```c++
// 对数组的引用
#include<iostream>
 using namespace std;
 int main(){
     int a[3]={1,2,3};
     int (&b)[3]=a;//对数组的引用 
     cout<<&a[0]<<" "<<&b[0]<<endl;
     cout<<&a[1]<<" "<<&b[1]<<endl;
     cout<<&a[2]<<" "<<&b[2]<<endl;
     return 0;
 }
console：
008FF790 008FF790
008FF794 008FF794
008FF798 008FF798
    
// 对指针的引用
#include<iostream>
using namespace std;
int main(){
    int a=10;
    int *ptr=&a;
    int *&new_ptr=ptr;
    cout<<&ptr<<" "<<&new_ptr<<endl;
    return 0; 
}
console：
006FF96C 006FF96C
```

```c++
#include<iostream>
using namespace std;
void Increment(int& a)
{
    a++;
    return;
}
int main() {
    int a = 10;
    Increment(a);
    cout << a << endl;
    return 0;
}
// 直接传引用 a的值会被修改
```

引用只是让代码更易读，没有任何事情是引用能做但指针不能做的；

```c++
	int b = 8;
    int& ref = a;
    ref = b;// 将b赋值给了a的引用
    cout << a << endl;
    cout << b << endl;
    cout << ref << endl;
console:
8
8
8
```



```c++
	int a = 10;
    int b = 8;
    int* ref = &a;
    *ref = 2;
    ref = &b;
    *ref = 1;
    cout << a << endl;
    cout << b << endl;
    cout << ref << endl;

console:
2
1
00B5FCAC
```



# 18 CLASSES in C++

面向对象编程只是你在编程时采用的一种风格关于如何编写你的代码；

（JAVA，C#也是面向对象语言）这些语言只适合面向对象编程；

而C++不仅仅支持面向对象编程（事实上C++支持，面向对象，基于对象，面向过程，泛型编程四种）

C语言不支持面向对象编程；

**类**

就是一种将数据和函数组织在一起的方式；

类不是万能的，而且类也没有提供什么特有的函数，能用类完成的同样也能不用类，所以C语言还存在，并且很好；

类的存在只是让程序员更轻松，只是糖衣语法，让你能够更好的去组织更好维护的代码而已！

```c++
#include<iostream>
using namespace std;
class Player
{
public:
    int x, y;
    int speed;
    void Move(int xa, int ya)
    {
        x += xa * speed;
        y += ya * speed;
    }
};

int main() {
    Player player;
    player.x = 1;
    player.y = 2;
    player.speed = 2;
    player.Move(2, 3);
    cout << player.x << endl;
    cout << player.y << endl;
    return 0;
}
// 这个类完全可以用C实现，并且包括了数据和函数！
```

# 19 CLASSES vs STRUCTS in C++

在C++中结构体和类的区别是什么？

唯一的区别：类默认是私有的，而struct默认是共有的！！

```c++
#include<iostream>
using namespace std;
struct Player
{
    int x, y;
    int speed;
    void Move(int xa, int ya)
    {
        x += xa * speed;
        y += ya * speed;
    }
};

int main() {
    Player player;
    player.x = 1;
    player.y = 2;
    player.speed = 2;
    player.Move(2, 3);
    cout << player.x << endl;
    cout << player.y << endl;
    return 0;
}
// 代码仍然能够执行，如果加private，就会像类一样报错了！
```



如何定义这两个词之间的差别：

作用上并没有太大区别，但是在代码实际使用时确实有所不同；

C++中结构体存在的唯一原因：想要维持与C之间的兼容性，因为C中没有类；

当然这种不兼容可以通过

#define struct class

来弥补，但是里面的public与private默认行为也是不好解决的；

两者使用，只是编程风格的问题：cherno的编程风格：

1. 当考虑一些plain old data时，他会尽可能多的使用struct；只代表一堆变量；即使有一些操作变量的函数；

2. 绝对不会对结构使用继承；仅仅想让struct是数据的结构；

# 20 How to Write a C++ Class



