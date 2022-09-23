# 输入输出相关

## Q：可以使得输入在不换行的情况下停止吗？

不可以，换行是输入结束的标志

## Q：如何输入输出汉字

首先请阅读[计算机基础知识1.1节](../useful-cs-knowledge/1.1-xin-xi-zai-ji-suan-ji-zhong-de-biao-shi.md#bian-ma)中编码相关内容，了解汉字如何在计算机中存储，汉字的编码问题。

### wchar\_t

类似char，在C++中存在双字节字符类型wchar\_t，分给单个字符的存储空间更大，单个wchar\_t 型变量还是一个字符型变量。例如，定义wchar\_t c = '好'是合法的，但wchar\_t c = 'ABC'则不合法。

```cpp
// wchat_t.cpp
#include<iostream>
#include<clocale>
using namespace std;
int main()
{
    //使用setlocale函数将本机的语言设置为中文简体
    setlocale(LC_ALL, "chs");//LC_ALL表示设置所有的选项（包括金融货币、小数点，时间日期格式、语言字符串的使用习惯等），chs表示中文简体
    wchar_t wt[] = L"中国你好！";//大写字母L告诉编译器为"中"字分配两个字节的空间
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

## Q：cout>>"hello">>"word"的输出为什么没有空格

空格也是字符，Ascii码值为32。在合适的位置添加即可。

（ by 倪士平）
