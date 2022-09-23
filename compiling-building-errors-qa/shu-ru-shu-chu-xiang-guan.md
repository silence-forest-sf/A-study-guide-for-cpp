# 输入输出相关

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
