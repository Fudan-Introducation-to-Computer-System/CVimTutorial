# C语言入门
> 往届是没有C语言入门的内容的，助教第一次试图做一个完整的、适合有Java基础的同学的教程。因为是摸索着前进，如果出现错误，请大家及时反馈，把这个教程做得更好。       —— 谢东方

## 第一个C程序
与Java不同，C语言中通过#include导入头文件/工具库，#include '库名'表示导入当前目录下的头文件，而#include <库名>表示导入系统路径下的头文件，你可以下载对应的头文件添加到你的gcc编译目录下，进行使用。另外，C中没有类的概念，通过main方法进行启动。
```shell
touch hello.c // 创建hello.c文件
vim hello.c // 编辑hello.c文件
```

```c
#include <stdio.h>
int main(int argc, char** argv) {
    printf("Hello C\n");
    return 0;
}

```

```
gcc hello.c -o hello // 进行编译，输出为hello文件
./hello // 运行该文件
```

## 输出
C语言的输出不像Java那么轻松，在java中使用syso就可以了，在C中则比较复杂。因为在C中Debug也不好用，所以需要我们多加入几句printf。另外，同学们自行谷歌/百度行缓冲和立即输出的区别。
```C
#include <stdio.h>

int main(int argc, char** argv) {
    fprintf(stderr, "输出错误\n");// stderr是立即输出的，输出到标准错误中，而stdout是标准输出
    printf("标准输出\n"); // 相当于fprintf(stdout, "标准错误\n")。
    float f = 1.0;
    printf("数字：%f\n", f);
    char str[] = "this is a string.\n";
    printf("%s", str);
    return 0;
}
```

## 数组的初始化与使用
看个例子，大家就懂了。
```C
#include <stdio.h>
int main(int argc, char** argv) {
    int nums[10];// 注意java里面是int[] nums = new int[10];
    for (int i = 0; i < 10 ; i++) {
        nums[i] = 12;
        printf("%d\n", nums[i]);
    }
    return 0;
}
```

## 条件判断
C中没有true和false，只有0和非0，0是false，非0是true。

## char数组与字符串
对于字符串的处理，头文件在string.h中。
参考：http://c.biancheng.net/view/337.html
```C
#include <stdio.h>
#include <string.h>

int main(int argc, char** argv) {
    char strA[] = "I am from China.";
    char strB[] = "No one knows China better than me.";
    if (strcmp(strA, strB)) {
        printf("Not equal.\n");
    }
    else printf("Equal.\n");
    return 0;
}
```

## 宏定义define和typedef
### 宏定义
宏定义经常用于定义简单函数，以加快效率。但是，宏定义仅仅相当于文本替换，所以要小心其中可能存在的错误。

```C
#include <stdio.h>
#define  MAX( x, y )  ( ((x) > (y)) ? (x) : (y) )
#define  MIN( x, y )  ( ((x) < (y)) ? (x) : (y) )
int main(int argc, char** argv) {
    printf("MAX(1,2) = %d\n", MAX(1, 2));
    printf("MIN(1,2) = %d\n", MIN(1, 2));
    return 0;
}

```
可能会出现的问题主要是由于，符号结合的先后顺序不一样，解决的方案是多加括号。
```C
#include <stdio.h>
#define SQUARE(x) (x)*(x)

int main(int argc, char** argv) {
    int a = 10;
    int b = SQUARE(a);
    printf("b: %d\n", b);
    int c = 100 / SQUARE(10); // c = 100
    printf("c: %d\n", c);
    return 0;
}

```
解决方案是#define SQUARE(x) ((x)*(x))

宏定义还会用于防止同一个头文件被重复导入的情况。
```C
#ifndef COMDEF_H
#define COMDEF_H

//头文件内容
#endif
```
当然宏定义还有很多内容，希望有兴趣的同学去了解一下。

### typedef的用法
typedef 也是为了程序员方便，不用写太多的代码。typedef，就是将原有的类型，换过一个名字。

```C
struct tagPoint
{
    double x;
    double y;
    double z;
};

typedef struct tagPoint Point
int main(int argc, char** argv) {
    Point p1={100,100,0};
    printf("p1.x = %f\n", p1.x);
    return 0;
}
```
其他内容，下次课再进行补充。



# Vim
## Vim的配置
参考： http://www.ruanyifeng.com/blog/2018/09/vimrc.html
<br/>
上面的链接是复杂版本的，但是一般情况下，我个人就只用前两行。特别要注意linux配置文件在.vimrc里面，而windows的配置文件在_vimrc里面。
```
set tabstop=2
set nu!

syntax enable
syntax on
set autoindent
```

## Vim的使用
参考： https://www.jianshu.com/p/8b679b35c9d5
* 注意区分命令行模式、插入模式、底行模式<br/>
    - 一般先通过命令touch file新建文件，再通过命令vim file进行编辑。
    - 通过点击i进行编辑，或者A从本行末尾开始编辑。
    - 退出编辑模式，要点击一下ESC键，然后输入 :wq进行保存，不保存用 :q!

* 查找
    - 通过点击Esc进入命令行模式，输入:/{关键字}进行查找。利用n键下一个，N键上一个。

* Cut & Paste 剪切与黏贴
    - 点击Esc进入命令行模式，输入比方说 10加上两次c键，就会截取10行，其他数字也可以。
    - 之后，找到一个地方，点击Esc进入命令行模式，按p键，就会把所有的内容黏贴进去。


## 作业
使用c语言，完成以下问题：
https://leetcode-cn.com/problems/string-to-integer-atoi/

