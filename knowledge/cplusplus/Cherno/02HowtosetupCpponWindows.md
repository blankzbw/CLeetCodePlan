# 1. VS and VS code

> 1. vscode是一个简洁的**文本编辑器**，占用空间不超过100M，但是在安装了插件之后可以做vs的大多数基础功能（自动补全，一键编译链接运行，错误提示，程序调试等）并且具备很好的跨平台性，支持windows，linux，mac版本.
> 2. vs是一个功能全面的集成开发环境，大约20G，开箱即用，编译工具，调试工具都是配置好的，目前只支持windows。下载链接：https://visualstudio.microsoft.com/zh-hans/vs/



# 2.安装VS2019

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

