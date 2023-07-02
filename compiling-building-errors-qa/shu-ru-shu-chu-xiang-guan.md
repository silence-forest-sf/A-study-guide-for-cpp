# 输入输出及运算相关

## Q：'\x40'，'\n'都是什么?

`\`表示对后面紧跟着的字符进行转义。如`\x40`是`@`，`@`的Ascii码值就是40，`\n`是换行符。

转义是值使得某个字符序列具有不同于该字符序列单独出现时的语义，转义字符的两个功能分别是：一，表示设备命令或者无法被字母表直接表示的特殊数据；二，字符引用，用于表示无法在当前上下文中被键盘录入的字符（如字符串中的回车符），或者在当前上下文中会有不期望的含义的字符（如C语言字符串中的双引号字符"，不能直接出现，必须用转义序列表示）

## Q：可以使得输入在不换行的情况下停止吗？

不可以，换行是输入结束的标志

（by 刘舒畅）

## Q：如何输入输出汉字

首先请阅读[计算机基础知识1.1节](../useful-cs-knowledge/1.1-xin-xi-zai-ji-suan-ji-zhong-de-biao-shi.md#bian-ma)中编码相关内容，了解汉字如何在计算机中存储，汉字的编码）问题。

### wchar\_t

类似char，在C++中存在双字节字符类型wchar\_t，分给单个字符的存储空间更大，单个wchar\_t 型变量还是一个字符型变量。例如，定义wchar\_t c = '好'是合法的，但wchar\_t c = 'ABC'则不合法，宽字符不等于字符串。

```cpp
// wchat_t.cpp
#include<iostream>
#include<clocale>
using namespace std;
int main()
{
    //使用setlocale函数将本机的语言设置为中文简体
    setlocale(LC_ALL, "chs");//LC_ALL表示设置所有的选项（包括金融货币、小数点，时间日期格式、语言字符串的使用习惯等），chs表示中文简体
    wchar_t wt[] = L"汉字输出测试";//大写字母L告诉编译器为"中"字分配两个字节的空间
    wcout << wt << endl;//使用wcout来代替cout输出宽字符，wcin类代替cin输入宽字符
    cout << wcslen(wt) << endl;//wcslen输出宽字符串的长度，输出长度是5
    cout << sizeof(wt) << endl;//输出长度是12个字节，最后的wchar_t类型的'\0'两个字节
    return 0;
}
```

上述代码在DevC++中直接运行会报错，原因在于编译器中编译选项对字符集配置存在问题，此处不做深究，有意愿的同学自行研究。

### string

string类是不定长度的，可以处理汉字这样的多字节编码的字符，需注意这里需要引入`#include<string>`，这个头文件中声明了string类和相关的方法,不同于`#include<cstring>`中对char数组的各种操作。

```
// wchat_t.cpp
#include<iostream>
#include<string>
using namespace std;
int main()
{
	string example="汉字输出测试";
	cout << example;
	return 0;
}
```

（ by 倪士平）

## Q：VScode输出汉字出现乱码

造成该问题的本质在于，vscode默认使用的是UTF-8,而Windows系统默认的编码则是GBK（也是cmd所使用的代码页），两者在字符的二进制指示上有很大区别，在运行过程中才会出现乱码。关于编码相关知识见1[.1节编码部分](../useful-cs-knowledge/1.1-xin-xi-zai-ji-suan-ji-zhong-de-biao-shi.md#bian-ma)

修改VScode的方法见[博客](https://blog.csdn.net/weixin\_46595440/article/details/125267724)

（by 倪士平 陈欣宇）

## Q：cout>>"hello">>"word"的输出为什么没有空格

空格也是字符，Ascii码值为32。在合适的位置添加即可。

（ by 倪士平）

## Q：如何查看符号位？

根据[有符号整数](../useful-cs-knowledge/1.1-xin-xi-zai-ji-suan-ji-zhong-de-biao-shi.md#you-fu-hao-shu-de-biao-shi)和[浮点数](../useful-cs-knowledge/1.1-xin-xi-zai-ji-suan-ji-zhong-de-biao-shi.md#fu-dian-shu-de-biao-shi)的相关知识，我们只需要将变量以二进制输出看第一位就行。下面给出了一个在C++中以不同形式输出整数的方法：

```cpp
#include <iostream>
#include <bitset> //输出二进制的头文件
using namespace std;
 
int main(){
	int a = -12333;
	cout << "八进制： " << oct << a << endl;
	cout << "十进制： " << dec << a << endl;
	cout << "十六进制： " << hex << a << endl;
	cout << "二进制： " << bitset<sizeof(a)*8>(a) << endl;
	return 0;
}
```

（by 刘舒畅 倪士平）

## Q：为什么表达式算出来不对/是小数？

很可能藏着数据类型的转换，C++中存在一些隐式的类型转换规则，在编码时需要注意。下面给出一些例子：

<figure><img src="../.gitbook/assets/数据类型导致计算错误.png" alt=""><figcaption></figcaption></figure>

这里`minutes`变量为int类型，除以整数所得结果仍为int。若想得到小数，至少使得参与运算的其中一个变量为浮点型。可将`minutes`定义为浮点型，或将`/60`改为`/60.0`。

（by 刘舒畅 倪士平）

## Q：为什么会有`warning C4305：“初始化”：从“double”到“float”截断`这样的警告？

在类型转换中，由于float和double类型的精度不同，因而double的数据不能完全存入float中，会从数据尾舍掉存储不下的部分。

（by 刘舒畅 倪士平）

## Q：如果我想要让两个整型变量相除的小数结果，要怎么做呢？

可通过强制类型转换将其中一方转换为浮点型。例：

```
int a=1,b=2; 
cout<<(double)a/b;
```

但要注意，类似`(double)(a/b)`的语句会将`(a/b)`这个整型数据转换为浮点型，而不会保留小数。

（by 刘舒畅 倪士平）

## Q：为什么这个表达式的运算结果不对

有以下几种原因：

1. 参与运算或者保存结果的**变量类型错误**
2. 使用了错误的函数或者运算符
   1. `||`是逻辑运算符，而\`|\`是与运算符
   2. \`^\`不是平方而是异或
3. 由于运算符优先级导致的问题

（by 倪士平 刘舒畅）

## Q：`++i`与`i++`的区别？

`++i`先令`i`自加一，然后返回`i`的值；`i++`则是先返回再自加一。例如下面的语句：

```cpp
int i = 1;
int k = i++;
i = 1;
int j = ++i;
```

在这个例子中，`k=1`，`j=2`。

（by 刘舒畅）

## Q：为什么`0<a<10`不发挥作用？

`0<a<10`在实际运行时，`0<a`会正常判断，但被判断`<10`的部分是`0<a`的返回值，而不是`a`。如果想实现数学上的判断，应当写成类似`0<a&&a<10`的形式。

（by 刘舒畅）

## Q：为什么字符串数组就能使用cout直接打印出来，而int型数组不行？

有趣的问题。iostream自带了针对char\*和string的重载operator<<定义，所以可以直接打印。

（by 刘舒畅）

