# 02 How to setup cpp on windows

### 1. VS and VS code

> 1. vscode是一个简洁的**文本编辑器**，占用空间不超过100M，但是在安装了插件之后可以做vs的大多数基础功能（自动补全，一键编译链接运行，错误提示，程序调试等）并且具备很好的跨平台性，支持windows，linux，mac版本.
> 2. vs是一个功能全面的集成开发环境，大约20G，开箱即用，编译工具，调试工具都是配置好的，目前只支持windows。下载链接：https://visualstudio.microsoft.com/zh-hans/vs/

## 2. 安装VS2019

> 1.选择社区community版本（free），安装时选择Desktop development with C++;
>
> 2.推荐一个插件：VISUAL ASSIST，能自动识别各种关键字，系统函数，成员变量，自动给出输入提示，自动更正大小写错误，自动标示错误等，可提升开发过程中的自动化和开发效率。
>
> 3.大佬的2019设置配置文件：/setting/ChernoVS.vssettings,导入配置：工具->导入和导出
>
> 4.how to your helloworld:创建一个C++项目，在源文件中添加一个Main.cpp 添加以下代码，右键项目名称->build(生成)；或者选择本地windows调试器直接编译运行。
>
> ```c++
> #include <iostream>
> int main()
> {
> 	std::cout << "hello,world!" << std::endl;
> 	std::cin.get();
> }
> ```

# 05 How C++ works

## 1. 生成可执行文件的流程

预处理（#），编译（编译成机器码），链接（将每个编译单元链接起来）

预处理：将头文件copy到cpp文件中；

编译	 ：仅编译cpp文件，将cpp文件编译成一个个的object文件（.obj）;当仅仅是编译一个文件的时候，需要当前文件即使用到其他文件的中的函数，也要有声明（就是说明这个函数存在）！否则编译报错！而如果你从未实现函数在其他文件中，那么就应该时链接时报错了。linker error

链接：将单独的.obj链接成.exe;(linker)工作：resolve symbols，联通各个函数；

unresolved external symbol ： linker无法解析一个symbol；

## 2.VS 界面

solution configration（编译配置？）：1. Debug；2.Release(区别在选择了不同的优化策略)

solution plaforms（编译平台）：X64 X86

项目右击属性（properties）：选择配置和平台，去build项目；其中Configuration Type：选择编译类型：Application（.exe）Dynamic Library(.dll) Static Library(.lib)

更多的更具体的错误信息要在output窗口查看，而不是error list。

## 3.VS快捷键

crtl+F7 ： build；compile（此时并不会链接）

# 06 How the C++ Compiler Works



comile：pre-process（预处理）、tokenzing(标记解释)、parsing（解析）

创建abstract syntax tree（抽象语法树）；

当编译器创建好抽象语法树后，就可以产生cpu会执行的代码了；

编译器的工作：1.把代码转化为constant data（常数资料）

​							2.把代码转化为instruction（指令）

C++里不像java要求类名和文件名一致，其实C++并不关心文件，文件的作用只是用来给编译器提供源码的某种方法；

需要告诉编译器文件类型和编译器该如何处理它，当创建一个.cpp时，编译器默认此后缀名要当成c++的文件进行处理；只是默认的习惯，是可以修改的；

translation unit  !=  .cpp （当CPP中include其他cpp时，其实就产生这一个.obj）

一个 translation unit产生一个.obj

预处理：

#include 只是将头文件中的代码copy过去

```c++
// zbw.h
}

// main.cpp
int main()
{
	int a = 0;
#include "zbw.h"
```

VS生成预处理文件中间件：

项目右击属性：选择C/C++、预处理、预处理到文件选则是即可；

编译后查看debug中的Main.i文件：

```c++
#line 1 "D:\\git\\vs2019\\FisrtProject\\FirstPro\\FirstPro\\Main.cpp"
int main()
{
	int a = 0;
#line 1 "D:\\git\\vs2019\\FisrtProject\\FirstPro\\FirstPro\\zbw.h"
}
#line 5 "D:\\git\\vs2019\\FisrtProject\\FirstPro\\FirstPro\\Main.cpp"
```

VS生成汇编代码：

项目右击属性：选择C/C++、输出文件、汇编程序输出选择仅有程序集的列表（/FA）；

```c++
//源码
int mul(int a, int b)
{
	return	a * b;
}
```

输出mul.asm文件

```c++
; Listing generated by Microsoft (R) Optimizing Compiler Version 19.29.30038.1 

	TITLE	D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Debug\Mul.obj
	.686P
	.XMM
	include listing.inc
	.model	flat

INCLUDELIB MSVCRTD
INCLUDELIB OLDNAMES

msvcjmc	SEGMENT
__2024AE0E_Mul@cpp DB 01H
msvcjmc	ENDS
PUBLIC	?mul@@YAHHH@Z					; mul
PUBLIC	__JustMyCode_Default
EXTRN	@__CheckForDebuggerJustMyCode@4:PROC
EXTRN	__RTC_CheckEsp:PROC
EXTRN	__RTC_InitBase:PROC
EXTRN	__RTC_Shutdown:PROC
;	COMDAT rtc$TMZ
rtc$TMZ	SEGMENT
__RTC_Shutdown.rtc$TMZ DD FLAT:__RTC_Shutdown
rtc$TMZ	ENDS
;	COMDAT rtc$IMZ
rtc$IMZ	SEGMENT
__RTC_InitBase.rtc$IMZ DD FLAT:__RTC_InitBase
rtc$IMZ	ENDS
; Function compile flags: /Odt
;	COMDAT __JustMyCode_Default
_TEXT	SEGMENT
__JustMyCode_Default PROC				; COMDAT
	push	ebp
	mov	ebp, esp
	pop	ebp
	ret	0
__JustMyCode_Default ENDP
_TEXT	ENDS
; Function compile flags: /Odtp /RTCsu /ZI
;	COMDAT ?mul@@YAHHH@Z
_TEXT	SEGMENT
_a$ = 8							; size = 4
_b$ = 12						; size = 4
?mul@@YAHHH@Z PROC					; mul, COMDAT
; File D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Mul.cpp
; Line 2
	push	ebp
	mov	ebp, esp
	sub	esp, 192				; 000000c0H
	push	ebx
	push	esi
	push	edi
	mov	edi, ebp
	xor	ecx, ecx
	mov	eax, -858993460				; ccccccccH
	rep stosd
	mov	ecx, OFFSET __2024AE0E_Mul@cpp
	call	@__CheckForDebuggerJustMyCode@4
; Line 3
	mov	eax, DWORD PTR _a$[ebp]
	imul	eax, DWORD PTR _b$[ebp]
; Line 4
	pop	edi
	pop	esi
	pop	ebx
	add	esp, 192				; 000000c0H
	cmp	ebp, esp
	call	__RTC_CheckEsp
	mov	esp, ebp
	pop	ebp
	ret	0
?mul@@YAHHH@Z ENDP					; mul
_TEXT	ENDS
END
```

编译器优化：

Debug模式不会进行任何优化，所以机器码也会很冗余；以保证易于进行debug；

VS调整优化规则：

项目右击属性：选择C/C++、优化、优化选择最大优化（优化速度）（/O2）；

由于O2和RTC1不兼容还要修改：

项目右击属性：选择C/C++、代码生成、基本运行时检查选择选择默认值；

在看上述源码优化后的结果

```c++
; Listing generated by Microsoft (R) Optimizing Compiler Version 19.29.30038.1 

	TITLE	D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Debug\Mul.obj
	.686P
	.XMM
	include listing.inc
	.model	flat

INCLUDELIB MSVCRTD
INCLUDELIB OLDNAMES

msvcjmc	SEGMENT
__2024AE0E_Mul@cpp DB 01H
msvcjmc	ENDS
PUBLIC	?mul@@YAHHH@Z					; mul
PUBLIC	__JustMyCode_Default
EXTRN	@__CheckForDebuggerJustMyCode@4:PROC
; Function compile flags: /Odt
;	COMDAT __JustMyCode_Default
_TEXT	SEGMENT
__JustMyCode_Default PROC				; COMDAT
	push	ebp
	mov	ebp, esp
	pop	ebp
	ret	0
__JustMyCode_Default ENDP
_TEXT	ENDS
; Function compile flags: /Ogtp
;	COMDAT ?mul@@YAHHH@Z
_TEXT	SEGMENT
_a$ = 8							; size = 4
_b$ = 12						; size = 4
?mul@@YAHHH@Z PROC					; mul, COMDAT
; File D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Mul.cpp
; Line 2
	push	ebp
	mov	ebp, esp
	mov	ecx, OFFSET __2024AE0E_Mul@cpp
	call	@__CheckForDebuggerJustMyCode@4
	mov	eax, DWORD PTR _a$[ebp]
	imul	eax, DWORD PTR _b$[ebp]
; Line 4
	pop	ebp
	ret	0
?mul@@YAHHH@Z ENDP					; mul
_TEXT	ENDS
END
```

修改一下，感受一下编译器的优化：

```c++
int mul()
{
	return	5 * 2;
}
```

mul.asm

```c++
; Listing generated by Microsoft (R) Optimizing Compiler Version 19.29.30038.1 

	TITLE	D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Debug\Mul.obj
	.686P
	.XMM
	include listing.inc
	.model	flat

INCLUDELIB MSVCRTD
INCLUDELIB OLDNAMES

msvcjmc	SEGMENT
__2024AE0E_Mul@cpp DB 01H
msvcjmc	ENDS
PUBLIC	?mul@@YAHXZ					; mul
PUBLIC	__JustMyCode_Default
EXTRN	@__CheckForDebuggerJustMyCode@4:PROC
; Function compile flags: /Odt
;	COMDAT __JustMyCode_Default
_TEXT	SEGMENT
__JustMyCode_Default PROC				; COMDAT
	push	ebp
	mov	ebp, esp
	pop	ebp
	ret	0
__JustMyCode_Default ENDP
_TEXT	ENDS
; Function compile flags: /Ogtp
;	COMDAT ?mul@@YAHXZ
_TEXT	SEGMENT
?mul@@YAHXZ PROC					; mul, COMDAT
; File D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Mul.cpp
	mov	ecx, OFFSET __2024AE0E_Mul@cpp
	call	@__CheckForDebuggerJustMyCode@4
	mov	eax, 10					; 0000000aH
	ret	0
?mul@@YAHXZ ENDP					; mul
_TEXT	ENDS
END
```

可以看到

mov	eax, 10					; 0000000aH

直接计算出了结果；

没有必要对于两个常数的乘法在运行时耗时计算，在编译阶段就计算好了，这就是常量折叠（constant folding）

在看一个优化更大的例子：

```c++
const char* Log(const char* message)
{
	return message;
}
int Multiply(int a , int b )
{
	Log("Multiply");
	return	a * b;
}
```

未优化前：

```c++
; Listing generated by Microsoft (R) Optimizing Compiler Version 19.29.30038.1 

	TITLE	D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Debug\Mul.obj
	.686P
	.XMM
	include listing.inc
	.model	flat

INCLUDELIB MSVCRTD
INCLUDELIB OLDNAMES

msvcjmc	SEGMENT
__2024AE0E_Mul@cpp DB 01H
msvcjmc	ENDS
PUBLIC	?Log@@YAPBDPBD@Z				; Log
PUBLIC	?Multiply@@YAHHH@Z				; Multiply
PUBLIC	__JustMyCode_Default
PUBLIC	??_C@_08EOBDLMOI@Multiply@			; `string'
EXTRN	@__CheckForDebuggerJustMyCode@4:PROC
;	COMDAT ??_C@_08EOBDLMOI@Multiply@
CONST	SEGMENT
??_C@_08EOBDLMOI@Multiply@ DB 'Multiply', 00H		; `string'
CONST	ENDS
; Function compile flags: /Odt
;	COMDAT __JustMyCode_Default
_TEXT	SEGMENT
__JustMyCode_Default PROC				; COMDAT
	push	ebp
	mov	ebp, esp
	pop	ebp
	ret	0
__JustMyCode_Default ENDP
_TEXT	ENDS
; Function compile flags: /Odtp /ZI
;	COMDAT ?Multiply@@YAHHH@Z
_TEXT	SEGMENT
_a$ = 8							; size = 4
_b$ = 12						; size = 4
?Multiply@@YAHHH@Z PROC					; Multiply, COMDAT
; File D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Mul.cpp
; Line 6
	push	ebp
	mov	ebp, esp
	sub	esp, 64					; 00000040H
	push	ebx
	push	esi
	push	edi
	mov	ecx, OFFSET __2024AE0E_Mul@cpp
	call	@__CheckForDebuggerJustMyCode@4
; Line 7
	push	OFFSET ??_C@_08EOBDLMOI@Multiply@
	call	?Log@@YAPBDPBD@Z			; Log
	add	esp, 4
; Line 8
	mov	eax, DWORD PTR _a$[ebp]
	imul	eax, DWORD PTR _b$[ebp]
; Line 9
	pop	edi
	pop	esi
	pop	ebx
	mov	esp, ebp
	pop	ebp
	ret	0
?Multiply@@YAHHH@Z ENDP					; Multiply
_TEXT	ENDS
; Function compile flags: /Odtp /ZI
;	COMDAT ?Log@@YAPBDPBD@Z
_TEXT	SEGMENT
_message$ = 8						; size = 4
?Log@@YAPBDPBD@Z PROC					; Log, COMDAT
; File D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Mul.cpp
; Line 2
	push	ebp
	mov	ebp, esp
	sub	esp, 64					; 00000040H
	push	ebx
	push	esi
	push	edi
	mov	ecx, OFFSET __2024AE0E_Mul@cpp
	call	@__CheckForDebuggerJustMyCode@4
; Line 3
	mov	eax, DWORD PTR _message$[ebp]
; Line 4
	pop	edi
	pop	esi
	pop	ebx
	mov	esp, ebp
	pop	ebp
	ret	0
?Log@@YAPBDPBD@Z ENDP					; Log
_TEXT	ENDS
END

```

可以发现Mul函数在做乘法前调用了Log

call	?Log@@YAPBDPBD@Z			; Log

imul	eax, DWORD PTR _b$[ebp]

开启优化O2？？？预期call会被优化掉，但是我的好像并没有被优化掉，但7line8line好像被合并了？

```c++
; Listing generated by Microsoft (R) Optimizing Compiler Version 19.29.30038.1 

	TITLE	D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Debug\Mul.obj
	.686P
	.XMM
	include listing.inc
	.model	flat

INCLUDELIB MSVCRTD
INCLUDELIB OLDNAMES

msvcjmc	SEGMENT
__2024AE0E_Mul@cpp DB 01H
msvcjmc	ENDS
PUBLIC	?Log@@YAPBDPBD@Z				; Log
PUBLIC	?Multiply@@YAHHH@Z				; Multiply
PUBLIC	__JustMyCode_Default
PUBLIC	??_C@_08EOBDLMOI@Multiply@			; `string'
EXTRN	@__CheckForDebuggerJustMyCode@4:PROC
;	COMDAT ??_C@_08EOBDLMOI@Multiply@
CONST	SEGMENT
??_C@_08EOBDLMOI@Multiply@ DB 'Multiply', 00H		; `string'
CONST	ENDS
; Function compile flags: /Odt
;	COMDAT __JustMyCode_Default
_TEXT	SEGMENT
__JustMyCode_Default PROC				; COMDAT
	push	ebp
	mov	ebp, esp
	pop	ebp
	ret	0
__JustMyCode_Default ENDP
_TEXT	ENDS
; Function compile flags: /Ogtp
;	COMDAT ?Multiply@@YAHHH@Z
_TEXT	SEGMENT
_a$ = 8							; size = 4
_b$ = 12						; size = 4
?Multiply@@YAHHH@Z PROC					; Multiply, COMDAT
; File D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Mul.cpp
; Line 6
	push	ebp
	mov	ebp, esp
	mov	ecx, OFFSET __2024AE0E_Mul@cpp
	call	@__CheckForDebuggerJustMyCode@4
	push	OFFSET ??_C@_08EOBDLMOI@Multiply@
	call	?Log@@YAPBDPBD@Z			; Log
	mov	eax, DWORD PTR _a$[ebp]
	add	esp, 4
	imul	eax, DWORD PTR _b$[ebp]
; Line 9
	pop	ebp
	ret	0
?Multiply@@YAHHH@Z ENDP					; Multiply
_TEXT	ENDS
; Function compile flags: /Ogtp
;	COMDAT ?Log@@YAPBDPBD@Z
_TEXT	SEGMENT
_message$ = 8						; size = 4
?Log@@YAPBDPBD@Z PROC					; Log, COMDAT
; File D:\git\vs2019\FisrtProject\FirstPro\FirstPro\Mul.cpp
; Line 2
	push	ebp
	mov	ebp, esp
	mov	ecx, OFFSET __2024AE0E_Mul@cpp
	call	@__CheckForDebuggerJustMyCode@4
	mov	eax, DWORD PTR _message$[ebp]
; Line 4
	pop	ebp
	ret	0
?Log@@YAPBDPBD@Z ENDP					; Log
_TEXT	ENDS
END

```

# 07 How the C++ Linker Works

链接：主要就是找到每个符号和函数的位置，并将它们链接到一起；

编译错误以C的开头

error C2143: 语法错误: 缺少“;”

链接错误以L开头：

 error LNK2019: 无法解析的外部符号 _main，函数 "

当编译.exe必须指定一个入口函数，但这个函数不一定时mian，可以自定义入口点；

项目右击属性：选择Linker、高级、入口点处设置；（未尝试）

Linker常见报错：

unresolved external symbol ：使用一个未在本文件实现的函数，并且进行了声明时，但是在链接过程中，并没有找到这个函数的实现；

static 静态函数：

表示这个函数只会被当前文件使用，不可能会被除本文件外的文件进行链接！

这样此静态函数即使调用了一个未在本文件实现的函数，进行了声明，但未在其他函数实现的函数时，链接也不会报错，但是如果不是静态函数，链接时会报错，因为并没有明确告诉链接器其他文件不存在使用这个函数的清空；如下：

```c++
const char* Log(const char* message);

int mul()
{
	Log("Multiply");
	return	1;
}
int main() 
{
	//mul();
}
```

编译不会报错，只会在链接时报错；

Mul.obj : error LNK2019: 无法解析的外部符号 "char const * __cdecl Log(char const *)" (?Log@@YAPBDPBD@Z)

```c++
const char* Log(const char* message);

static int mul()
{
	Log("Multiply");
	return	1;
}
int main() 
{
	//mul();
}
```

编译不会报错，链接也不会报错；

Linker常见报错：

函数被重复实现（不是在一个文件里面实现两次，这种编译就会报错，而是头文件有函数实现，并且头文件被不小心include两次）

只要头文件里面只有声明，就会避免这个错误。

# 11 How to DEBUG C++ in VS

DEBUG：暂停程序，看内存；

一个正在运行的程序的内存几乎就是它的全部；

step into 进入到函数；F11

step over 到当前函数的下一行代码；F10

step out 跳出当前函数；shift+F11

调试过程中三个重要的窗口：

Autos 展示重要的变量

Locals 展示局部变量

Watch 实时监控变量

调处内存视图：DEBUG->Windows->内存->内存1

调式模式：编译器会让程序做一些让我们便于调试的事情；

举例：

内存是cc的，意味着他是一个未初始化的堆栈内存；（cc = 204）因为编译器知道我们要创建一个变量，当还未初始化的时候，就会用cc来填充内存；

# 12 CONDITIONS and BRANCHES in C++

使用disassemblely处理代码

调式过程中，右击代码->转到反汇编：(一定不要编译的时候进行优化，否则一些信息就会丢失)

```c++
	bool compRet = c == 2;
	if (compRet)
	{
		c = 3;
	}
```

反汇编如下：

```c++
bool compRet = c == 2;
00D743AF  cmp         dword ptr [c],2  
00D743B3  jne         __$EncStackInitStart+55h (0D743C1h)  
00D743B5  mov         dword ptr [ebp-104h],1  
00D743BF  jmp         __$EncStackInitStart+5Fh (0D743CBh)  
00D743C1  mov         dword ptr [ebp-104h],0  
00D743CB  mov         al,byte ptr [ebp-104h]  
00D743D1  mov         byte ptr [compRet],al  
	if (compRet)
00D743D4  movzx       eax,byte ptr [compRet]  
00D743D8  test        eax,eax  
00D743DA  je          __$EncStackInitStart+77h (0D743E3h)  
	{
		c = 3;
00D743DC  mov         dword ptr [c],3  
	}
```

jne:jump not equal ;

# 13 BEST VS Step for C++ Project !

配置项目中生成文件的路径：

项目右击属性：选择常规；

将配置和平台选择成对所有的均生效；

输出目录：$(SolutionDir)bin\$(Platform)\$(Configuration)\

中间目录：$(SolutionDir)bin\intermediates\$(Platform)\$(Configuration)\

