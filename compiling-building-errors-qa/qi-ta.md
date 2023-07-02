# 编译相关

## Q：为什么要写using namesapce std；

C++的STL都是定义在std命名空间中的， using namespace语句的作用是提前声明要引 用的命名空间，这样引用命名空间中的名称时就不用加命名空间前缀。 例如，如果不写using namespace std的话，在引用cin的时候，就要写成std::cin。（刘舒畅 倪士平）

## Q：为什么要写xxxx头文件

你所使用的某个函数或某个类在xxxx头文件中声明的，有时候你不写也能用的原因可能是已经写明的头文件中交叉引用了xxx头文件。

（ by 倪士平）

## Q：“LNK1168无法打开xxx文件进行写入”

与已经执行的任务冲突，检查一下是否已经打开了一个调试窗口，或存在其他程序打开了xxx文件

（ by 倪士平 刘舒畅）

## Q："无法启动程序‘xxx.exe’系统找不到指定文件"

检查你的代码文件是否在项目的“源代码”文件夹下，检查的方法就是看VS右侧“解决方案资源管理器”

<img src="../.gitbook/assets/image (2).png" alt="" data-size="original">

找不到则在“视图”下查找，点击“解决方案资源管理器”后将出现在屏幕右侧。

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

（ by 倪士平）

## Q："mingw-w64-crt/crt/crt0\_c.c:18: undefined reference to 'WinMain' "

检查一下你的main打对了没有。

（by 倪士平）

## Q：为什么同一份代码使用两种编译器的结果会不一样？

| clang                              | gcc                                |
| ---------------------------------- | ---------------------------------- |
| ![](../.gitbook/assets/编译器区别1.jpg) | ![](../.gitbook/assets/编译器区别2.jpg) |

这里使用了一个可能没有被C++语言规范 规定的语句： a=a++。这里产生一个问题，是赋原来的a，还是赋加之后的a。你使用的VS使用的底层编译器是clang，而你使用的在线IDE的编译器是gcc，两者对这一语句做出不同的判断。

（by 刘舒畅 倪士平）



## Q：在包含头文件时，报错提示No such file or directory

有以下几种原因：

1. 命名时或者包含头文件时名字打错了
2. 没有指明包含文件的路径或者没有把头文件放在同一个文件夹下

（by 倪士平）

