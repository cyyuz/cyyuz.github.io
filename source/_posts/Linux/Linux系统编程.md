---
title: Linux命令
date: 2024-06-18 11:12:56
tags: [linux, vim]
categories:
- [技术, linux]
---


# vim

<table>
    <tr> 
        <th>功能</th>
        <th>操作</th> 
        <th>描述</th> 
    </tr>
    <tr>
        <td rowspan="3"> 撤销 </td> 
        <td>u</td>
        <td> 撤销最近的操作，多次按下，撤销多个操作 </td>
    </tr>
    <tr>
        <td>Ctrl+r</td>
        <td> 恢复上一步被撤销的操作 </td>
    </tr>
    <tr>
        <td>:u!</td>
        <td> 撤销所有修改 </td>
    </tr>
    <tr>  
        <td rowspan="12"> 光标移动 </td>
        <td>h</td>
        <td> 向左移动一个字符 </td>
    </tr>
    <tr>
        <td>l</td>
        <td> 向右移动一个字符 </td>
    </tr>
    <tr>
        <td>j</td>
        <td> 向下移动一行 </td>
    </tr>
    <tr>
        <td>k</td>
        <td> 向上移动一行 </td>
    </tr>
    <tr>
        <td>b</td>
        <td> 向前移动一个单词 </td>
    </tr>
    <tr>
        <td>w</td>
        <td> 向后移动一个单词 </td>
    </tr>
    <tr>
        <td>e</td>
        <td> 光标跳转到本单词的尾部 </td>
    </tr>
    <tr>
        <td>0</td>
        <td> 移动到行首 </td>
    </tr>
    <tr>
        <td>$</td>
        <td> 移动到行尾 </td>
    </tr>
    <tr>
        <td>gg</td>
        <td> 移动到首行 </td>
    </tr>
    <tr>
        <td>GG</td>
        <td> 移动到末行 </td>
    </tr>
    <tr>
        <td>:n</td>
        <td> 光标移动到第n行 </td>
    </tr>
    <tr> 
        <td rowspan="4"> 翻页 </td>
        <td>Ctrl+b</td>
        <td> 向上翻一页 </td>
    </tr>
    <tr>
        <td>Ctrl+f</td>
        <td> 向下翻一页 </td>
    </tr>
    <tr>
        <td>Ctrl+u</td>
        <td> 向上翻半页 </td>
    </tr>
    <tr>
        <td>Ctrl+d</td>
        <td> 向下翻半页 </td>
    </tr>
    <tr>  
        <td rowspan="5"> 查找 </td>
        <td>/test</td>
        <td> 查找test </td>
    </tr>
    <tr>
        <td>n</td>
        <td> 下一个查找内容 </td>
    </tr>
    <tr>
        <td>N</td>
        <td> 上一个查找内容 </td>
    </tr>
    <tr>
        <td>/\ctest</td>
        <td> 忽略大小写，查找test </td>
    </tr>
    <tr>
        <td>/\btest</td>
        <td> 查找整个单词，而不是部分匹配 </td>
    </tr>
    <tr>  
        <td rowspan="6"> 插入 </td>
        <td>i</td>
        <td> 在光标所在位置前面插入 </td>
    </tr>
    <tr>
        <td>a</td>
        <td> 在光标所在位置后面插入 </td>
    </tr>
    <tr>
        <td>o</td>
        <td> 在光标所在行的下面插入空白行</td>
    </tr>
    <tr>
        <td>O</td>
        <td> 在光标所在行的上面插入空白行 </td>
    </tr>
    <tr>
        <td>I</td>
        <td> 在光标所在行的行首插入 </td>
    </tr>
    <tr>
        <td>A</td>
        <td> 在光标所在行的行末插入 </td>
    </tr>
    <tr>  
        <td rowspan="5"> 剪切</td>
        <td>x</td>
        <td> 剪切光标所在位置的一个字符 </td>
    </tr>
    <tr>
        <td>3x</td>
        <td> 剪切光标所在位置开始的3个字符 </td>
    </tr>
    <tr>
        <td>dw</td>
        <td> 剪切光标所在位置到本单词结尾的字符 </td>
    </tr>
    <tr>
        <td>D</td>
        <td> 剪切本行光标所在位置后的全部内容 </td>
    </tr>
    <tr>
        <td>3dd</td>
        <td> 剪切光标所在行开始的3行 </td>
    </tr>
        <tr>  
        <td rowspan="2"> 复制</td>
        <td>yy</td>
        <td> 光标所在行复制到缓冲区 </td>
    </tr>
    <tr>
        <td>3yy</td>
        <td> 光标所在行开始的3行复制到缓冲区 </td>
    </tr>
    </tr>
        <tr>  
        <td rowspan="2"> 粘贴</td>
        <td>p</td>
        <td> 将缓冲区里的内容粘贴到光标所在位置 </td>
    </tr>
    <tr>
        <td>:set paste</td>
        <td> 粘贴模式，不自动换行 </td>
    </tr>
    </tr>
        <tr>  
        <td rowspan="4"> 替换</td>
        <td>r</td>
        <td> 替换光标所在位置的一个字符 </td>
    </tr>
    <tr>
        <td>R</td>
        <td>从光标所在位置开始替换字符，按Esc结束</td>
    </tr>
    <tr>
        <td>cw</td>
        <td>从光标所在位置开始替换单词，按Esc结束</td>
    </tr>
    <tr>
        <td>:%s/aaa/bbb/g</td>
        <td>把文件中全部的aaa替换成bbb</td>
    </tr>
    <tr>  
        <td rowspan="2"> 可视</td>
        <td>v</td>
        <td> 把当前行的下一行接到当前行的尾部 </td>
    </tr>
    <tr>
        <td>Ctrl+V</td>
        <td>列操作</td>
    </tr>
    <tr>  
        <td rowspan="5"> 退出</td>
        <td>:w</td>
        <td> 保存 </td>
    </tr>
    <tr>
        <td>:w!</td>
        <td>强制保存</td>
    </tr>
    <tr>
        <td>:wq | :x</td>
        <td>保存退出</td>
    </tr>
    <tr>
        <td>:q</td>
        <td>退出</td>
    </tr>
    <tr>
        <td>:q!</td>
        <td>不保存，强制退出</td>
    </tr>
    <tr>  
        <td rowspan="4"> 其他</td>
        <td>J</td>
        <td> 把当前行的下一行接到当前行的尾部 </td>
    </tr>
    <tr>
        <td>Ctrl+g</td>
        <td>显示光标所在位置的行号和文件的总行数</td>
    </tr>
    <tr>
        <td>.</td>
        <td>重复执行上一次执行的vi命令</td>
    </tr>
    <tr>
        <td>~</td>
        <td>对光标当前所在的位置的字符进行大小写转换</td>
    </tr>
</table>

# 编译

## gcc/g++

```shell
gcc/g++ [选项] source1.cpp source2.cpp
```

| 选项       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| -o         | 指定输出的文件名，名称不能和源文件同名。默认为a.out。        |
| -g         | 如果想对源代码进行调试，必须加入这个选项。                   |
| -c         | 只编译，不链接成为可执行文件，通常用于把源文件编译成静态库或动态库。 |
| -On        | 在编译、链接过程中进行优化处理，生成的可执行程序效率将更高。 |
| -std=c++11 | 支持C++11标准。                                              |

- 优化选项：

| 选项    | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| -O0     | 不做任何优化，这是默认的编译选项。                           |
| -O或-O1 | 对程序做部分编译优化，对于大函数，优化编译占用稍微多的时间和相当大的内存。使用本项优化，编译器会尝试减小生成代码的尺寸，以及缩短执行时间，但并不执行需要占用大量编译时间的优化。 |
| -O2     | **推荐的优化等级**。与O1比较而言，O2优化增加了编译时间的基础上，提高了生成代码的执行效率。 |
| -O3     | 这是最高最危险的优化等级。用这个选项会延长编译代码的时间，并且在使用gcc4.x的系统里不应全局启用。自从3.x版本以来gcc的行为已经有了极大地改变。在3.x，-O3生成的代码也只是比-O2快一点点而已，而gcc4.x中还未必更快。用-O3来编译所有的软件包将产生更大体积更耗[内存](https://so.csdn.net/so/search?q=内存&spm=1001.2101.3001.7020)的二进制文件，大大增加编译失败的机会或不可预知的程序行为（包括错误）。这样做将得不偿失，记住过犹不及。在gcc 4.x.中使用-O3是不推荐的。 |

如果使用了优化选项：1）编译的时间将更长；2）目标程序不可调试；3）有效果，但是**不可能显著提升程序的性能**。

## 静态库和动态库

### 静态库

- 编译

```sh
g++ -c -o libxxx.a source1.cpp source2.cpp
```

- 使用静态库

```sh
g++ [选项] 源代码文件名清单 -l库名 -L库文件所在的目录名
```

- 静态库的概念

程序在编译时会把库文件的二进制代码链接到目标程序中，这种方式称为静态链接。

如果多个程序中用到了同一静态库中的函数或类，就会存在多份拷贝。

- 静态库的特点
  - 静态库的链接是在编译时期完成的，执行的时候代码加载速度快。
  - 目标程序的可执行文件比较大，浪费空间。
  - 程序的更新和发布不方便，如果某一个静态库更新了，所有使用它的程序都需要重新编译。

### 动态库

- 制作动态库

```sh
g++ -fPIC -shared -o lib库名.so 源代码文件清单
```

- 使用动态库

```sh
g++ 选项 源代码文件名清单 -l库名 -L库文件所在的目录名
```

运行可执行程序的时候，需要提前设置 `LD_LIBRARY_PATH` 环境变量。

- 动态库的概念

程序在编译时不会把库文件的二进制代码链接到目标程序中，而是在运行时候才被载入。

如果多个进程中用到了同一动态库中的函数或类，那么在内存中只有一份，避免了空间浪费问题。

- 动态库的特点
  - 程序在运行的过程中，需要用到动态库的时候才把动态库的二进制代码载入内存。
  - 可以实现进程之间的代码共享，因此动态库也称为共享库。
  - 程序升级比较简单，不需要重新编译程序，只需要更新动态库就行了。
- 如果动态库和静态库同时存在，编译器将优先使用动态库。

## makefile

## gdb

如果希望程序可调试，编译时需要加 `-g` 选项，并且，不能使用 `-O` 的优化选项。

- 常用命令

| 命令     | 简写 | 命令说明                                                     |
| -------- | ---- | ------------------------------------------------------------ |
| set args |      | 设置程序运行的参数。                                         |
| break    | b    | 设置断点，`b 20`表示在第20行设置断点，可以设置多个断点。     |
| run      | r    | 开始运行程序，运行到断点会停下来，如果没有遇到断点，程序一直运行下去。 |
| next     | n    | 执行当前行语句，如果该语句为函数调用，不会进入函数内部。 VS的F10 |
| step     | s    | 执行当前行语句，如果该语句为函数调用，则进入函数内部。VS的F11。如果函数是库函数或第三方提供的函数，用s也是进不去的，因为没有源代码，如果是自定义的函数，只要有源码就可以进去。 |
| print    | p    | 显示变量或表达式的值，如果p后面是表达式，会执行这个表达式。  |
| continue | c    | 继续运行程序，遇到下一个断点停止，如果没有遇到断点，程序将一直运行。VS的F5 |
| set var  |      | 设置变量的值。                                               |
| quit     | q    | 退出gdb。                                                    |

注意：在gdb中，用上下光标键可以选择执行过的gdb命令。

- 调试core文件

如果程序在运行的过程中发生了内存泄漏，会被内核强行终止，提示“段错误（吐核）”，内存的状态将保存在core文件中，方便程序员进一步分析。

Linux缺省不会生成core文件，需要修改系统参数。

调试core文件的步骤如下：

1）用ulimit -a查看当前用户的资源限制参数；

2）用ulimit -c unlimited把core file size改为unlimited；

3）运行程序，产生core文件；

4）运行gdb 程序名 core文件名；

5）在gdb中，用bt查看函数调用栈。

- 调试正在运行的程序

```sh
gdb programe -p PID
```

## main函数参数

main函数有三个参数，argc、argv和envp，它的标准写法如下：

```c++
int main(int argc,char *argv[],char *envp[])
{
    return 0;
}
```

| 参数 | 描述                                   |
| ---- | -------------------------------------- |
| argc | 存放程序参数的个数，包括程序本身。     |
| argv | 存放每个参数的值，包括程序本身。       |
| envp | 存放环境变量，数组的最后一个元素是空。 |

- 设置环境变量

int setenv(const char *name, const char *value, int overwrite);

name     环境变量名。

value     环境变量的值。

overwrite  0-如果环境不存在，增加新的环境变量，如果环境变量已存在，不替换其值；非0-如果环境不存在，增加新的环境变量，如果环境变量已存在，替换其值。

返回值：0-成功；-1-失败（失败的情况极少见）。

注意：此函数设置的环境变量只对本进程有效，不会影响shell的[环境变量](https://baike.baidu.com/item/环境变量?fromModule=lemma_inlink)。如果在运行程序时执行了setenv()函数，进程终止后再次运行该程序，上次的设置是无效的。

- 获取环境变量的值

char *getenv(const char *name);

# Linux命令

## man

**1-用户命令**；2-系统接口；**3-库函数**；4-特殊文件，比如设备文件；5-文件；

6-游戏；7-系统的软件包；8-系统管理命令；9-内核。

## ln



## scp

## ulimit 



# Linux时间操作

UNIX操作系统根据计算机产生的年代把1970年1月1日作为UNIX的纪元时间，1970年1月1日是时间的中间点，将从1970年1月1日起经过的秒数用一个整数存放。

## time_t

`time_t` 用于表示时间类型，是 `long` 类型的别名，表示从1970年1月1日0时0分0秒到现在的秒数。

## time()

`time()` 库函数用于获取操作系统的当前时间。

```c
#include <time.h>

// 声明
time_t time(time_t *tloc);

// 1.将空地址传递给time()函数，并将time()返回值赋给变量now。
time_t now = time(0);  

// 2.将变量now的地址作为参数传递给time()函数。
time_t now; 
time(&now); 
```

## struct tm

`time_t` 是一个长整数，需要转换成 `tm` 结构体，`tm` 结构体在中声明，如下：        

```c
#include <time.h>

struct tm{
    int tm_year;  // 年份：其值等于实际年份减去1900
    int tm_mon;  // 月份：取值区间为[0,11]，其中0代表一月，11代表12月
    int tm_mday; // 日期：一个月中的日期，取值区间为[1,31]
    int tm_hour;  // 时：取值区间为[0,23]
    int tm_min;  // 分：取值区间为[0,59]
    int tm_sec;   // 秒：取值区间为[0,59]
    int tm_wday; // 星期：取值区间为[0,6]，其中0代表星期天，6代表星期六
    int tm_yday;  // 从每年的1月1日开始算起的天数：取值区间为[0,365] 
    int tm_isdst;  // 夏令时标识符，该字段意义不大
}
```

## localtime()

`localtime()` 函数用于把 `time_t` 表示的时间转换为 `tm` 结构体表示的时间。

`localtime()` 函数不是线程安全的，`localtime_r()` 是线程安全的。

```c
#include <time.h>

// 函数声明：
struct tm *localtime(const time_t *timep);
struct tm *localtime_r(const time_t *timep, struct tm *result);
```

示例：

```c++
#include <iostream>
#include <time.h>

int main() {
    time_t time_ = time(0);
    tm ltm_;
    localtime_r(&time_, &ltm_);
    printf("time = %d-%d-%d %d:%d:%d\n", ltm_.tm_year + 1900, ltm_.tm_mon + 1, ltm_.tm_mday, ltm_.tm_hour, ltm_.tm_min, ltm_.tm_sec);
}
```

## mktime()

`mktime()` 函数的功能与 `localtime()` 函数相反，用于把 `tm` 结构体时间转换为 `time_t` 时间。

函数声明：

```c++
time_t mktime(struct tm *tm);
```

该函数主要用于时间的运算，例如：把2022-03-01 00:00:25加30分钟。

思路：

1. 解析字符串格式的时间，转换成tm结构体；
2. 用mktime()函数把tm结构体转换成time_t时间；
3. 把time_t时间加30*60秒；
4. 用localtime_r()函数把time_t时间转换成tm结构体；
5. 把tm结构体转换成字符串。

## gettimeofday()

用于获取1970年1月1日到现在的秒和当前秒中已逝去的微秒数，可以用于程序的计时。

函数声明：

```c++
int gettimeofday(struct timeval *tv, struct timezone *tz);

struct timeval {
    time_t      tv_sec;    /* 1970-1-1到现在的秒数 */
    suseconds_t tv_usec;   /* 当前秒中，已逝去的微秒数 */
};

struct timezone {     /* 时区，在实际开发中，派不上用场 */
    int tz_minuteswest;    /* minutes west of Greenwich */ 
    int tz_dsttime;        /* type of DST correction */
};
```

示例：

```c++
#include <sys/time.h>
#include <iostream>

int main(){
    timeval start, end;
    gettimeofday(&start, NULL);
    for(int i = 0; i < 100000000; i++){
        // do nothing
    }
    gettimeofday(&end, NULL);
    std::cout << "Time elapsed: " << (end.tv_sec - start.tv_sec) * 1000000 + (end.tv_usec - start.tv_usec) << " us" << std::endl;
}
```

## sleep()

声明：

```c++
unsigned int sleep(unsigned int seconds);
int usleep(useconds_t usec);
```

示例：

```c++
#include <unistd.h>

int main(){
    sleep(1);     // 1s
    usleep(1000); // 1s
}
```

# Linux文件操作

## 获取当前工作目录

声明：

```c++
char *getcwd(char *buf, size_t size); 
char *get_current_dir_name(void);
```

示例：

```c++
#include <iostream>
#include <unistd.h>

int main() {
    // getcwd
    char path1[256];   // 256 is the maximum length of a path in Linux
    getcwd(path1, sizeof(path1));
    std::cout << "path1=" << path1 << std::endl;
	
    // get_current_dir_name
    char* path2 = get_current_dir_name();
    std::cout << "path2=" << path2 << std::endl;
    free(path2);   // free the memory allocated by get_current_dir_name()
}
```

## 切换工作目录

函数声明：

```c++
int chdir(const char *path);
```

> 返回值：0-成功；其它-失败（目录不存在或没有权限）。

示例：

```c++
#include <iostream>
#include <unistd.h>

int main() {
    char path[256];   // 256 is the maximum length of a path in Linux
    getcwd(path, sizeof(path));
    std::cout << "path=" << path << std::endl;

    if (0 != chdir("..")) {   // change directory to parent directory
        std::cout << "chdir failed" << std::endl;
    }

    getcwd(path, sizeof(path));
    std::cout << "path=" << path << std::endl;
}
```

## 创建目录

函数声明

```c++
/**
 * @brief 创建目录
 * @param pathname 目录名。
 * @param mode 访问权限，如0755，不要省略前置的0。
 * @return 0-成功；其它-失败（上级目录不存在或没有权限）。
*/
int mkdir(const char *pathname, mode_t mode);
```

## 删除目录

函数声明：

```c++
/**
 * @brief 删除目录
 * @param path-目录名。
 * @return 0-成功；其它-失败（目录不存在或没有权限）。
*/
int rmdir(const char *path);
```

## 获取目录中文件的列表

文件存放在目录中，在处理文件之前，必须先知道目录中有哪些文件，所以要获取目录中文件的列表。

函数声明：

```c++
/**
 * @brief 打开目录
 * @param pathname-目录名。
 * @return 成功-返回目录的地址，失败-返回空地址。
*/
DIR *opendir(const char *pathname);

/**
 * @brief 读取目录
 * @param dirp-目录指针。
 * @return 成功-返回struct dirent结构体的地址，失败-返回空地址。
*/
struct dirent *readdir(DIR *dirp);

/** 
 * @brief 关闭目录
 * @param dirp-目录指针。
 * @return 0-成功；其它-失败。
*/
int closedir(DIR *dirp);
```
数据结构
```c++
/**
 * @brief 目录指针
*/
DIR *dir;

/**
 * @brief 目录项
 * @param d_ino 索引节点号。
 * @param d_off 在目录文件中的偏移。
 * @param d_reclen 文件名长度。
 * @param d_type 文件类型。有多种取值，最重要的是8和4，8-常规文件（A regular file）；4-子目录（A directory）。注意，d_name的数据类型是字符，不可直接显示。
 * @param d_name 文件名或目录名，最长255字符。
*/
struct dirent {
    long d_ino;                 
    off_t d_off;                 
    unsigned short d_reclen;      
    unsigned char d_type;        
    char d_name[NAME_MAX+1];
};
```

示例：

```c++
#include <dirent.h>
#include <iostream>

int main(int argc, char* argv[]) {
    if (argc != 2) {
        std::cout << "Usage: " << argv[0] << " <directory>" << std::endl;
        return -1;
    }
    DIR* dir;
    if ((dir = opendir(argv[1])) == nullptr) {
        std::cout << "Error: open directory " << argv[1] << " failed" << std::endl;
        return -1;
    }
    struct dirent* entry = nullptr;
    while ((entry = readdir(dir)) != nullptr) {
        std::cout << "文件名:" << entry->d_name << ", 文件类型:" << entry->d_type << std::endl;
    }
    closedir(dir); 
}
```

# Linux系统错误

在C++程序中，如果调用了库函数，可以通过函数的返回值判断调用是否成功。其实，还有一个整型的全局变量errno，存放了函数调用过程中产生的错误代码。

如果调用库函数失败，可以通过errno的值来查找原因，这也是调试程序的一个重要方法。

errno在<errno.h>中声明。

配合 strerror()和perror()两个库函数，可以查看出错的详细信息。

## strerror()

strerror() 在<string.h>中声明，用于获取错误代码对应的详细信息。

char *strerror(int errnum);               // 非线程安全。

int strerror_r(int errnum, char *buf, size_t buflen);    // 线程安全。

gcc8.3.1一共有133个错误代码。

示例一：

\#include <iostream>

\#include <cstring>

using namespace std;

 

int main()

{

 int ii;

 

 for(ii=0;ii<150;ii++)    // gcc8.3.1一共有133个错误代码。

 {

  cout << ii << ":" << strerror(ii) << endl;

 }

}

示例二：

\#include <iostream>

\#include <cstring>

\#include <cerrno>

\#include <sys/stat.h>

using namespace std;

 

int main()

{

 int iret=mkdir("/tmp/aaa",0755);

 

 cout << "iret=" << iret << endl;

 cout << errno << ":" << strerror(errno) << endl;

}

## perror()

perror() 在<stdio.h>中声明，用于在控制台显示最近一次系统错误的详细信息，在实际开发中，服务程序在后台运行，通过控制台显示错误信息意义不大。（对调试程序略有帮助）

void perror(const char *s);

## 注意事项

- 调用库函数失败不一定会设置errno

并不是全部的库函数在调用失败时都会设置errno的值，以man手册为准（一般来说，不属于系统调用的函数不会设置errno，属于系统调用的函数才会设置errno）。什么是系统调用？百度“库函数和系统调用的区别”。

- errno不能作为调用库函数失败的标志

errno的值只有在库函数调用发生错误时才会被设置，当库函数调用成功时，errno的值不会被修改，不会主动的置为 0。

在实际开发中，判断函数执行是否成功还得靠函数的返回值，只有在返回值是失败的情况下，才需要关注errno的值。

示例：

\#include <iostream>

\#include <cstring>  // strerror()函数需要的头文件。

\#include <cerrno>   // errno全局变量的头文件。

\#include <sys/stat.h> // mkdir()函数需要的头文件。

using namespace std;

 

int main()

{

 int iret=mkdir("/tmp/aaa/bb/cc/dd",0755);

 if (iret!=0)

 {

  cout << "iret=" << iret << endl;

  cout << errno << ":" << strerror(errno) << endl;

  perror("调用mkdir(/tmp/aaa/bb/cc/dd)失败");

 }

 

 iret=mkdir("/tmp/dd",0755);

 if (ireet!=0)

 {

  cout << "iret=" << iret << endl;

  cout << errno << ":" << strerror(errno) << endl;

  perror("调用mkdir(/tmp/dd)失败");

 }

}

# 目录文件更多操作

## access()库函数

access()函数用于判断当前用户对目录或文件的存取权限。

包含头文件：

\#include <unistd.h>

函数声明：

int access(const char *pathname, int mode);

参数说明：

pathname 目录或文件名。

mode     需要判断的存取权限。在头文件<unistd.h>中的预定义如下：

\#define R_OK  4  // 判断是否有读权限。

\#define W_OK 2  // 判断是否有写权限。

\#define X_OK  1  // 判断是否有执行权限。

\#define F_OK  0  // 判断是否存在。

返回值：

当pathname满足mode权限返回0，不满足返回-1，errno被设置。

在实际开发中，access()函数主要用于判断目录或文件是否存在。

## stat()库函数

### 1）stat结构体

struct stat结构体用于存放目录或文件的详细信息，如下：

struct stat

{

 dev_t st_dev;    // 文件的设备编号。

 ino_t st_ino;     // 文件的i-node。

 mode_t st_mode; // 文件的类型和存取的权限。

 nlink_t st_nlink;  // 连到该文件的硬连接数目，刚建立的文件值为1。

 uid_t st_uid;     // 文件所有者的用户识别码。

 gid_t st_gid;     // 文件所有者的组识别码。

 dev_t st_rdev;    // 若此文件为设备文件，则为其设备编号。

 off_t st_size;     // 文件的大小，以字节计算。

 size_t st_blksize;  // I/O 文件系统的I/O 缓冲区大小。

 size_t st_blocks;  // 占用文件区块的个数。

 time_t st_atime;  // 文件最近一次被存取或被执行的时间，

​               // 在用mknod、 utime、read、write 与tructate 时改变。

 time_t st_mtime;  // 文件最后一次被修改的时间，

​               // 在用mknod、 utime 和write 时才会改变。

 time_t st_ctime;  // 最近一次被更改的时间，在文件所有者、组、 权限被更改时更新。

};

struct stat结构体的成员变量比较多，重点关注st_mode、st_size和st_mtime成员。注意：st_mtime是一个整数表示的时间，需要程序员自己写代码转换格式。

st_mode成员的取值很多，用以下两个宏来判断：

S_ISREG(st_mode) // 是否为普通文件，如果是，返回真。 

S_ISDIR(st_mode) // 是否为目录，如果是，返回真。

### 2）stat()库函数

包含头文件：

\#include <sys/stat.h>

函数声明：

int stat(const char *path, struct stat *buf);

stat()函数获取path参数指定目录或文件的详细信息，保存到buf结构体中。

返回值：0-成功，-1-失败，errno被设置。

示例：

\#include <stdio.h>

\#include <iostream>

\#include <cstdio>

\#include <sys/stat.h>

\#include <unistd.h>

using namespace std;

 

int main(int argc,char *argv[])

{

 if (argc != 2) { cout << "Using:./demo 文件或目录名\n"; return -1; }

 

 struct stat st; // 存放目录或文件详细信息的结构体。

 

 // 获取目录或文件的详细信息

 if (stat(argv[1],&st) != 0)

 {

  cout << "stat(" << argv[1] << "):" << strerror(errno) << endl; return -1;

 }

 

 if (S_ISREG(st.st_mode))

  cout << argv[1] << "是一个文件(" << "mtime=" << st.st_mtime << ",size=" << st.st_size << ")\n";

 if (S_ISDIR(st.st_mode))

cout << argv[1] << "是一个目录(" << "mtime=" << st.st_mtime << ",size=" << st.st_size << ")\n";

}

## 三、utime()库函数

utime()函数用于修改目录或文件的时间。

包含头文件：

\#include <sys/types.h>

\#include <utime.h>

函数声明：

int utime(const char *filename, const struct utimbuf *times);

utime()函数用来修改参数filename的st_atime和st_mtime。如果参数times为空地址，则设置为当前时间。结构utimbuf 声明如下：

struct utimbuf

{

 time_t actime;

 time_t modtime;

};

返回值：0-成功，-1-失败，errno被设置。

## 四、rename()库函数

rename()函数用于重命名目录或文件，相当于操作系统的mv命令。

包含头文件：

\#include <stdio.h>

函数声明：

int rename(const char *oldpath, const char *newpath);

参数说明：

oldpath   原目录或文件名。

newpath  目标目录或文件名。

返回值：0-成功，-1-失败，errno被设置。

## 五、remove()库函数

remove()函数用于删除目录或文件，相当于操作系统的rm命令。

包含头文件：

\#include <stdio.h>

函数声明：

int remove(const char *pathname);

参数说明：

pathname 待删除的目录或文件名。

返回值：0-成功，-1-失败，errno被设置。

# Linux信号

信号（signal）是软件中断，是进程之间相互传递消息的一种方法，用于通知进程发生了事件，但是，不能给进程传递任何数据。

服务程序运行在后台，如果想让中止它，杀掉不是个好办法，因为进程被杀的时候，是突然死亡，没有安排善后工作。如果向服务程序发送一个信号，服务程序收到信号后，调用一个函数，在函数中编写善后的代码，程序就可以有计划的退出。如果向服务程序发送0的信号，可以检测程序是否存活。

在Shell中，可以用kill和killall命令发送信号：

```sh
kill -9 PID
killall -9 进程名
```

- **信号类型** 

| 信号名      | 信号值 | 默认处理动作 | 发出信号的原因                                         |
| ----------- | ------ | ------------ | ------------------------------------------------------ |
| SIGHUP      | 1      | A            | 终端挂起或者控制进程终止                               |
| **SIGINT**  | **2**  | **A**        | **键盘中断Ctrl+c**                                     |
| SIGQUIT     | 3      | C            | 键盘的退出键被按下                                     |
| SIGILL      | 4      | C            | 非法指令                                               |
| SIGABRT     | 6      | C            | 由abort(3)发出的退出指令                               |
| SIGFPE      | 8      | C            | 浮点异常                                               |
| **SIGKILL** | **9**  | **AEF**      | **采用kill  -9 进程编号 强制杀死程序。**               |
| **SIGSEGV** | **11** | **CEF**      | **无效的内存引用（数组越界、操作空指针和野指针等）。** |
| SIGPIPE     | 13     | A            | 管道破裂，写一个没有读端口的管道。                     |
| **SIGALRM** | **14** | **A**        | **由闹钟alarm()函数发出的信号。**                      |
| **SIGTERM** | **15** | **A**        | **采用“kill  进程编号”或“killall 程序名”通知程序。**   |
| SIGUSR1     | 10     | A            | 用户自定义信号1                                        |
| SIGUSR2     | 12     | A            | 用户自定义信号2                                        |
| **SIGCHLD** | **17** | **B**        | **子进程结束信号**                                     |
| SIGCONT     | 18     |              | 进程继续（曾被停止的进程）                             |
| SIGSTOP     | 19     | DEF          | 终止进程                                               |
| SIGTSTP     | 20     | D            | 控制终端（tty）上按下停止键                            |
| SIGTTIN     | 21     | D            | 后台进程企图从控制终端读                               |
| SIGTTOU     | 22     | D            | 后台进程企图从控制终端写                               |
| 其它        | <=64   | A            | 自定义信号                                             |

处理动作一项中的字母含义如下：

A 缺省的动作是终止进程。

B 缺省的动作是忽略此信号，将该信号丢弃，不做处理。

C 缺省的动作是终止进程并进行内核映像转储（core dump）。

D 缺省的动作是停止进程，进入停止状态的程序还能重新继续，一般是在调试的过程中。

E 信号不能被捕获。

F 信号不能被忽略。

## 信号的处理 

进程对信号的处理方法有三种：

1）对该信号的处理采用系统的默认操作，大部分的信号的默认操作是终止进程。

2）设置信号的处理函数，收到信号后，由该函数来处理。

3）忽略某个信号，对该信号不做任何处理，就像未发生过一样。

signal()函数可以设置程序对信号的处理方式。

函数声明：

sighandler_t signal(int signum, sighandler_t handler);

参数signum表示信号的编号（信号的值）。

参数handler表示信号的处理方式，有三种情况：

1）SIG_DFL：恢复参数signum信号的处理方法为默认行为。 

2）一个自定义的处理信号的函数，函数的形参是信号的编号。

3）SIG_IGN：忽略参数signum所指的信号。

## 信号应用示例 

\#include <iostream>

\#include <unistd.h>

\#include <signal.h>

using namespace std;

 

void EXIT(int sig)

{

 cout << "收到了信号：" << sig << endl;

 cout << "正在释放资源，程序将退出......\n";

 

 // 以下是释放资源的代码。

 

 cout << "程序退出。\n";

 exit(0); // 进程退出。

}

 

int main(int argc,char *argv[])

{

 // 忽略全部的信号，防止程序被信号异常中止。

 for (int ii=1;ii<=64;ii++) signal(ii,SIG_IGN);

 

 // 如果收到2和15的信号（Ctrl+c和kill、killall），本程序将主动退出。

 signal(2,EXIT); signal(15,EXIT);

 

 while (true)

 {

  cout << "执行了一次任务。\n";

  sleep(1);

 }

}

## 发送信号

Linux操作系统提供了kill和killall命令向进程发送信号，在程序中，可以用kill()函数向其它进程发送信号。

函数声明：

int kill(pid_t pid, int sig);

kill()函数将参数sig指定的信号给参数pid 指定的进程。

参数pid 有几种情况：

1）pid>0 将信号传给进程号为pid 的进程。

2）pid=0 将信号传给和当前进程相同进程组的所有进程，常用于父进程给子进程发送信号，注意，发送信号者进程也会收到自己发出的信号。

3）pid=-1 将信号广播传送给系统内所有的进程，例如系统关机时，会向所有的登录窗口广播关机信息。

sig：准备发送的信号代码，假如其值为0则没有任何信号送出，但是系统会执行错误检查，通常会利用sig值为零来检验某个进程是否仍在运行。

返回值说明： 成功执行时，返回0；失败返回-1，errno被设置。

# 进程

## 进程终止

有8种方式可以中止进程，其中5种为正常终止，它们是：

1）在 `main()` 函数用 `return` 返回；

2）在任意函数中调用` exit()` 函数；

3）在任意函数中调用 `_exit()` 或 `_Exit()` 函数；

4）最后一个线程从其启动例程（线程主函数）用 `return` 返回；

5）在最后一个线程中调用 `pthread_exit()` 返回；

异常终止有3种方式：

6）调用 `abort()` 函数中止；

7）接收到一个信号；

8）最后一个线程对取消请求做出响应。

- **进程终止的状态**

在 `main()` 函数中，`return` 的返回值即终止状态，如果没有 `return` 语句或调用 `exit()` ，那么该进程的终止状态是 `0` 。

在Shell中，查看进程终止的状态：`echo $?`

正常终止进程的3个函数（`exit()` 和 `_Exit()` 是由ISO C说明的，`_exit()` 是由POSIX说明的）。

```c++
void exit(int status);
void _exit(int status);
void _Exit(int status);
```

status也是进程终止的状态。

如果进程被异常终止，终止状态为非0。

- **资源释放的问题**

`retun` 表示函数返回，会调用局部对象的析构函数，`main()` 函数中的 `return` 还会调用全局对象的析构函数。

`exit()` 表示终止进程，不会调用局部对象的析构函数，只调用全局对象的析构函数。

`exit()` 会执行清理工作，然后退出，`_exit()` 和 `_Exit()` 直接退出，不会执行任何清理工作。

- **进程的终止函数**

进程可以用 `atexit()` 函数登记终止函数（最多32个），这些函数将由 `exit()` 自动调用。

函数声明：

```c++
int atexit(void (*function)(void));
```

exit()调用终止函数的顺序与登记时相反。 