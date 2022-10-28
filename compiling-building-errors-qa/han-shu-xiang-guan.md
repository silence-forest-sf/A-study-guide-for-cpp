# 函数相关

## Q：为什么VS提示scanf是不安全的

围绕scanf函数存在多种攻击方式，利用其输入长度不受限制等特性，可以实施缓冲区溢出、格式化字符串攻击等等，VS提供了scanf\_s函数弥补其安全性缺陷，但这不是标准函数，在其他编译器下是不存在。

在项目属性编辑ctrsecurenowarnings屏蔽掉安全警告的方法是不推荐的，相当于面对安全漏洞视而不见，装聋作哑。

（by 倪士平）

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
