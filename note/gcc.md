# Gcc

> reference : [知乎_Gcc](https://zhuanlan.zhihu.com/p/76930507)

## 什么是Gcc

gcc的全称是GNU Compiler Collection，它是一个能够编译多种语言的编译器。最开始gcc是作为C语言的编译器（GNU C Compiler），现在除了c语言，还支持C++、java、Pascal等语言。gcc支持多种硬件平台。

## 编译过程

1. 预处理（Pre-Processing）
2. 编译 （Compiling）
3. 汇编 （Assembling）
4. 链接 （Linking)

> reference: [知乎_编译]([C/C++语言编译链接过程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/88255667))

![v2-38aedd85719aa8828ba5ab912b7591b3_b.jpg](https://raw.githubusercontent.com/geraltigas/image/master/2022/02/23-18-47-21-v2-38aedd85719aa8828ba5ab912b7591b3_b.jpg)

##### 预处理

还是好理解

##### 编译

好理解

##### 汇编

也好理解, 可能是最简单的部分

##### 链接

对于写程序的人来说最复杂的部分

1. 如何链接

对于每个编译单元(.cpp), 有两种依赖, 一种是在文件中以声明 并且 已定义的函数 变量 , 还有一种就是 已声明 但 未定义, 他们依赖于外部定义. 而链接, 就解决了外部定义的问题

2. 静态库原理

静态库其实(不严谨来说), 就相当于别人帮你完成编译过程, 而链接部分提供给用户自己进行.因此, 我们需要.h文件(告诉我们自己的编译单元,存在这种函数或变量), 在链接时, 静态库文件就能被链接了.

打破固定思维的用法

```cpp
#include <iostream>


extern "C" int some_include_func();


int main() {
    int a = some_include_func();
    return 1;
}
```

假设现在有一个静态库, 头文件中有许多函数生命, 我们并不想包含所有定义, 就可以如上一样指定函数添加(如果是C语言,要加`extern "C"`, 因为符号表c与cpp不一样), 这样linker就能找到静态库中的函数了.综上可以看出, 静态库其实就是一种.o文件, 只是不是我们编译的.(这其实也解决了如何制作静态库的问题) 

3. 动态库原理

动态库就是把链接过程延迟到了可执行文件运行,或者是动态库函数被调用(lazy link).

但是不同寻常的是, 存在一个 `dll_namedll.lib`文件, 这个文件保存了所有动态库函数和变量的相对地址, 方便快速使用, 所有动态链接之前, 还要静态链接这个lib文件才能正常使用.
