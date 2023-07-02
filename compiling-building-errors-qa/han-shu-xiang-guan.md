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

## Q：C6262 函数使用堆叠的“40004”字节。请考虑将一些数据迁移到堆

<pre class="language-cpp"><code class="lang-cpp">// 来自同学的真实错误代码
#include&#x3C;iostream>
using namespace std;
int sum(int n){
    int a[10000];/开一个足够大的数组
    if(n>0)//输入
    cin >a[n - 1];
    if(n > 1)//递归条件
        return a[n -1] + sum(n -1);
    if(n == 1)/递归终止条件
        return a[0]
int main(){
    int n;
    cin >> n;
    cout &#x3C;&#x3C; sum(n);
    return 0;
<strong>}
</strong></code></pre>

报错信息意思是在“栈”里面占用了太多内存，原因是函数中定义的数组a过大，将其改为全局变量或使用指针分配空间都可。

在计算机内存中存在两种空间，一种是栈，一种是堆，**函数内声明的局部变量都在栈上**，调用函数便在这个内存栈上进行了分配空间操作即创建了一个栈帧，**操作系统对每个栈帧的大小做了限制，所以不能创建很大的数组**，声明为全局变量时则没有栈帧大小的限制。而堆空间可以进行自由分配，空间充足。

（by 倪士平 刘舒畅）

## Q：Run-Time Check Failure #2 - Stack around the variable 'arr' was corrupted.

```cpp
// 来自同学的真实错误代码
#include<iostream>

int main(){
    using namespace std;
    int i;
    int arr[] = {4, 2, 8, 0, 5, 7, 1, 3, 9};
    int mid;
    for(i = 0; i < 9; i++){
        if(arr[i] > arr[i+1]){
            mid = arr[i+1];
            arr[i+1] = arr[i];
            arr[i] = mid;
        }
    }
    for(i = 0; i < 9; i++){
        cout << arr;
    }
    return 0;
}
```

直接翻译报错信息：运行时检查失败#2-变量“arr”周围的堆栈已损坏

具体而言就是`arr[i+1]`会访问\`arr\[9]\`，这是未被定义的区域，故发生访问越界，这会触发一些编译的检查或者引出操作系统抛出异常。
