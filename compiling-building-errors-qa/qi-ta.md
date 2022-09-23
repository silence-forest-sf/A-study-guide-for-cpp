# 其他

## Q：为什么要写using namesapce std；

C++的STL都是定义在std命名空间中的， using namespace语句的作用是提前声明要引 用的命名空间，这样引用命名空间中的名称时就不用加命名空间前缀。 例如，如果不写using namespace std的话，在引用cin的时候，就要写成std::cin。（刘舒畅 倪士平）

## Q：为什么要写xxxx头文件

你所使用的某个函数或某个类在xxxx头文件中声明的，有时候你不写也能用的原因可能是已经写明的头文件中交叉引用了xxx头文件。

（ by 倪士平）

## Q：“LNK1168无法打开xxx文件进行写入”

检查一下是否已经打开了一个调试窗口，或存在其他程序打开了xxx文件

（ by 倪士平）

## Q："无法启动程序‘xxx.exe’系统找不到指定文件"

检查你的代码文件是否在项目的“源代码”文件夹下，检查的方法就是看VS右侧“解决方案资源管理器”

<img src="../.gitbook/assets/image (2).png" alt="" data-size="original">

找不到则在“视图”下查找，点击“解决方案资源管理器”后将出现在屏幕右侧。

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

（ by 倪士平）

## Q:"mingw-w64-crt/crt/crt0\_c.c:18: undefined reference to 'WinMain' "

检查一下你的main打对了没有。

（by 倪士平）
