# 数组相关

## Q：我们知道""内括入字符串代表着存储这些字符串的内存起始地址。然而cout<<"字符串"的结果会把这个字符串内容打印出来，也就是说向cout输出流中输入地址后，他应该打印出来的是这个地址对应的内存所存储的值。但cout<<&a则打印出来就是a变量存储的地址。
## Q：进一步的，用取址运算符取出a的地址后，假如是0x61feec，再cout<<0x61feec，结果打印出来又是整数，并非a的值。
## Q：cout的上述变化是为什么？

简言之，出现上述现象的原因是"cout <<"语句输出的特性取决于其中运算符<<右侧的操作数类型。针对以下三种操作数类型，其默认输出效果不同：
1. cout << 字符数组/字符指针/字符变量地址：此时默认输出字符数组中存储的字符串/字符指针指向的字符串/以字符变量地址为起始地址的内存片段中存储的字符串（注意区分概念“字符串”与“字符数组”）
2. cout << 之后的操作数是其它类型变量的数组/指针变量：此时默认输出十六进制表示的数组内存起始地址值/指针变量存储的地址值
3. cout << 之后的操作数是写入程序代码的十六进制数值：此时默认以十进制方式输出所指定的十六进制整数

cout是一种C++对象，上述特性体现了C++对象的多态性。用C语言可以实现类似的特性，但或须在C代码中进行频繁的显式类型转换，或须通过额外参数明确指定操作数类型，不能完全达到C++代码“以不变应万变”的效果。



上述现象的深层原理是C++运算符重载机制。语句"cout << 操作数"实质是调用运算符重载函数ostream& operator<<(ostream& os, type x)，其中第一实参为cout，第二实参为操作数。

C++库文件自带上述运算符重载函数operator<<的一系列形参类型不同的重载：
1. ostream& operator<<(ostream& os, const char *s)
2. ostream& operator<<(ostream& os, const int *s)
3. ostream& operator<<(ostream& os, const long *s) // 及其它类似定义
4. ostream& operator<<(ostream& os, const int x)
4. ostream& operator<<(ostream& os, const long x) // 及其它类似定义

在编译阶段，编译器根据实参"操作数"判断实际调用的重载函数，进行针对性的处理。因此，
1. 将语句"cout << 字符数组str/字符指针str"编译为重载函数ostream& operator<<(ostream& os, const char *s)的调用operator<<(cout, str)，该重载函数调用功能是输出字符数组str中存储的字符串/字符指针str指向的字符串；
2. 将语句"cout << 整型数组p/整型指针p"编译为重载函数ostream& operator<<(ostream& os, const int *s)的调用operator<<(cout, p)，该重载函数调用功能是输出十六进制表示的整型数组p内存起始地址值/整型指针p存储的地址值。以其它非字符型数组/指针为操作数的cout语句编译和功能与此类似。
3. 将语句"cout << 0x61feec"编译为重载函数ostream& operator<<(ostream& os, const int x)的调用operator<<(cout, 0x61feec)，该重载函数调用功能近似于将十六进制整数0x61feec转换为十进制，再输出。注意直接写入代码的0x61feec是十六进制表示的整型字面常量，默认情形下并不会被识别为内存地址值。

（by 郭淳）







## Q：为什么rand()输出的结果是固定的

先看一个样例代码

```cpp
//rand.cpp
#include<iostream>
#include<cstdlib>
using namespace std;
int main()
{
    int out = rand();
    cout << out;
    return 0;
}
```

反复编译运行上述代码会发现输出结果是固定的，原因在于随机函数rand()需要种子以生成随机序列，可以通过srand函数设置随机的种子，常见的做法就是设定当前时间为种子。

```cpp
// right_rand.cpp
#include<iostream>
#include<cstdlib>
#include<ctime>
using namespace std;
int main()
{
    srand(time(0));
    int out = rand();
    cout << out;
    return 0;
}
```

关于随机函数，计算机中的随机数大多都是伪随机，由某种算法进行计算得来，因此也会引入各种安全问题。

（by 倪士平）
