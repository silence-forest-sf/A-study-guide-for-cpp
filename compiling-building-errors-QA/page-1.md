# Page 1 郭淳

# 1.1 Visual Studio工程建立阶段的常见错误

在这一章中……

或应包括

选错项目类型

还有什么？

## 进制……

计算机

## 字节序……




# 1.2 第一个程序的常见错误

在这一章中……

或应包括

写错#include

写错关键字

写错printf、cout等标识符

写错main

写丢大括号




# 通过报错信息检索
# 1.3 错误	LNK2019	无法解析的外部符号 _main





# 1.4 错误	LNK2019	无法解析的外部符号 _main

详细信息：
错误	LNK2019	无法解析的外部符号 _main，该符号在函数 "int __cdecl invoke_main(void)" (?invoke_main@@YAHXZ) 中被引用	Integral	C:\Users\DELL\source\repos\Integral\MSVCRTD.lib(exe_main.obj)	1

简解：
出错原因是当前操作的Cpp工程/项目（Cpp project）中，没有任何一个\*.cpp源代码文件中正确书写了main函数（回顾第一课：如果希望编译出可执行程序，则必须书写main函数）。

初学阶段往往一个Cpp工程/项目只包含一个\*.cpp源代码文件，此时出错原因即为**该\*.cpp源代码文件中没有正确书写main函数**。进一步的，可能的书写错误包括：

1. 单词int或单词main拼写错误，例如拼写为mian； 
2. 单词int或单词main错用大写字母，例如拼写为Main（回顾课堂示例）；
3. 99999

此时应**仔细检查所写cpp源代码文件**，确认所犯错误是以上哪一种。



解析：

1. 错误代码LNK2019的前缀是LNK，顾名思义这是“链接”阶段发生的错误（回顾第一课课件），
2. 444
3. 555
4. 666
5. 777
6. 888
