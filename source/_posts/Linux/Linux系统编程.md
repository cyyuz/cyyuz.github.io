---
title: Linux系统编程
date: 2024-06-18 11:12:56
tags: [linux]
categories:
- [技术, linux]
---

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

main函数声明：

```c++
/**
 * @brief main函数
 * @param argc 参数个数，包括程序本身
 * @param argv 参数值，包括程序本身
 * @param envp 环境变量，数组的最后一个元素是空
 * @return 0
 */
int main(int argc,char *argv[],char *envp[])
{
    return 0;
}
```

- **设置环境变量**

函数声明：

```c++
/**
 * @brief 设置环境变量
 * @param name 环境变量名
 * @param value 环境变量的值
 * @param overwrite 0-如果环境不存在，增加新的环境变量，如果环境变量已存在，不替换其值；非0-如果环境不存在，增加新的环境变量，如果环境变量已存在，替换其值。
 * @return 0-成功；-1-失败（失败的情况极少见）
 */
int setenv(const char *name, const char *value, int overwrite);
```

**注意：**此函数设置的环境变量只对本进程有效，不会影响shell的环境变量。如果在运行程序时执行了 `setenv()` 函数，进程终止后再次运行该程序，上次的设置是无效的。

- **获取环境变量的值**

```c++
/**
 * @brief 获取环境变量的值
 * @param name 环境变量名
 * @return 环境变量的值，如果环境变量不存在，返回NULL
 */
char *getenv(const char *name);
```

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

函数声明：

```c++
/**
 * @brief 获取操作系统的当前时间
 * @param tloc 保存时间的变量，如果为空，函数返回当前时间，不保存。
 * @return 当前时间
 */
time_t time(time_t *tloc);
```

示例：

```c
#include <time.h>

// 1.将空地址传递给time()函数，并将time()返回值赋给变量now。
time_t now = time(0);  

// 2.将变量now的地址作为参数传递给time()函数。
time_t now; 
time(&now); 
```

## localtime()

**函数声明：**

```c
/**
 * @brief 把time_t表示的时间转换为tm结构体表示的时间，不是线程安全的
 * @param timep time_t表示的时间
 * @return tm结构体表示的时间
 */
struct tm *localtime(const time_t *timep);
/**
 * @brief 把time_t表示的时间转换为tm结构体表示的时间，线程安全
 * @param timep time_t表示的时间
 * @param result 保存tm结构体表示的时间
 * @return tm结构体表示的时间
 */
struct tm *localtime_r(const time_t *timep, struct tm *result);
```

**数据结构：**

`time_t` 是一个长整数，需要转换成 `tm` 结构体。

```c
/**
 * @brief 时间结构体
 * @param tm_year 年份：其值等于实际年份减去1900
 * @param tm_mon 月份：取值区间为[0,11]，其中0代表一月，11代表12月
 * @param tm_mday 日期：一个月中的日期，取值区间为[1,31]
 * @param tm_hour 时：取值区间为[0,23]
 * @param tm_min 分：取值区间为[0,59]
 * @param tm_sec 秒：取值区间为[0,59]
 * @param tm_wday 星期：取值区间为[0,6]，其中0代表星期天，6代表星期六
 * @param tm_yday 从每年的1月1日开始算起的天数：取值区间为[0,365] 
 * @param tm_isdst 夏令时标识符，该字段意义不大
 */
struct tm{
    int tm_year; 
    int tm_mon;
    int tm_mday; 
    int tm_hour;  
    int tm_min;
    int tm_sec;  
    int tm_wday; 
    int tm_yday;  
    int tm_isdst; 
}
```

**示例：**

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

**函数声明：**

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

**函数声明：**

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

**示例：**

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

**函数声明：**

```c++
unsigned int sleep(unsigned int seconds);
int usleep(useconds_t usec);
```

**示例：**

```c++
#include <unistd.h>

int main(){
    sleep(1);     // 1s
    usleep(1000); // 1s
}
```

# Linux文件操作

## 获取当前工作目录

**函数声明：**

```c++
char *getcwd(char *buf, size_t size); 
char *get_current_dir_name(void);
```

**示例：**

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

**函数声明：**

```c++
/**
 * @brief 切换工作目录
 * @param path-目录名。
 * @return 0-成功；其它-失败（目录不存在或没有权限）。
*/
int chdir(const char *path);
```

**示例：**

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

**函数声明：**

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

**函数声明：**

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

**函数声明：**

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
**数据结构：**

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

**示例：**

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
## access()

**函数声明：**

```c++
/**
 * @brief 检查当前用户是否可以访问文件
 * @param pathname-目录或文件名。
 * @param mode-需要判断的存取权限。
 * @return 0-成功；-1-失败，errno被设置。
*/
int access(const char *pathname, int mode);
```

**mode参数取值：**

```c++
#define R_OK  4  // 判断是否有读权限。
#define W_OK  2  // 判断是否有写权限。
#define X_OK  1  // 判断是否有执行权限。
#define F_OK  0  // 判断是否存在。
```

在实际开发中，access()函数主要用于判断目录或文件是否存在。

## stat()

**函数声明：**

```c++
/**
 * @brief 获取目录或文件的详细信息
 * @param path-目录或文件名。
 * @param buf-存放目录或文件的详细信息。
 * @return 0-成功，-1-失败，errno被设置。
*/
int stat(const char *path, struct stat *buf);
```

**数据结构：**

```c++
/**
 * @brief 存放目录或文件的详细信息。
*/
struct stat{
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
    time_t st_atime;  // 文件最近一次被存取或被执行的时间，在用mknod、 utime、read、write 与tructate 时改变。
    time_t st_mtime;  // 文件最后一次被修改的时间，在用mknod、 utime 和write 时才会改变。
    time_t st_ctime;  // 最近一次被更改的时间，在文件所有者、组、 权限被更改时更新。
};
```

重点关注 `st_mode`、`st_size` 和 `st_mtime` 成员。注意：`st_mtime` 是一个整数表示的时间，需要自己写代码转换格式。

`st_mode` 成员的取值很多，用以下两个宏来判断：

```c++
/**
 * @brief 判断文件类型
 * @param st_mode-文件类型和权限。
 * @return 如果是普通文件，返回真。
*/
S_ISREG(st_mode)
/**
 * @brief 判断是否为目录
 * @param st_mode-文件类型和权限。
 * @return 如果是目录，返回真。
*/
S_ISDIR(st_mode)
```

**示例：**

```c++
#include <iostream>
#include <string.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

int main(int argc, char* argv[]) {
    if (argc != 2) {
        std::cerr << "Usage: " << argv[0] << " <path>" << std::endl;
        return -1;
    }
    struct stat buf;
    if (stat(argv[1], &buf) == -1) {
        std::cerr << "stat(" << argv[1] << "): " << strerror(errno) << std::endl;
        return -1;
    }

    if (S_ISREG(buf.st_mode)) {
        std::cout << "Regular file" << std::endl;
    }
    else if (S_ISDIR(buf.st_mode)) {
        std::cout << "Directory" << std::endl;
    }
}
```

## utime()

**函数声明：**

```c++
/**
 * @brief 修改文件最后访问和修改时间（st_atime和st_mtime）
 * @param filename 文件名
 * @param times 修改的时间，如果为空，则设置为当前时间
 * @return 0-成功，-1-失败，errno被设置
 */
int utime(const char *filename, const struct utimbuf *times);
```

**数据结构：**

```c++
/**
 * @brief 修改文件最后访问和修改时间（st_atime和st_mtime）
 */
struct utimbuf
{
    time_t actime;
    time_t modtime;
};
```

## rename()

**函数声明：**

```c++
/**
 * @brief 重命名目录或文件
 * @param oldpath 原目录或文件名
 * @param newpath 目标目录或文件名
 * @return 0-成功，-1-失败，errno被设置
 */
int rename(const char *oldpath, const char *newpath);
```

## remove()

**函数声明：**

```c++
/**
 * @brief 删除文件或目录
 * @param pathname 待删除的文件或目录名
 * @return 0-成功，-1-失败，errno被设置
 */
int remove(const char *pathname);
```

# Linux系统错误

整型的全局变量 `errno`，存放了函数调用过程中产生的错误代码。如果调用库函数失败，可以通过errno的值来查找原因，这也是调试程序的一个重要方法。

## strerror()

**函数声明：**

```c++
/**
 * @brief 获取错误代码对应的详细信息
 * @param errnum 错误代码
 * @return 错误信息字符串
 * @note 非线程安全。
*/
char *strerror(int errnum); 

/**
 * @brief 获取错误代码对应的详细信息
 * @param errnum 错误代码
 * @param buf 存放错误信息的缓冲区
 * @param buflen 缓冲区大小
 * @return 错误信息字符串
 * @note 线程安全。
*/
int strerror_r(int errnum, char *buf, size_t buflen); 

/**
 * @note gcc8.3.1一共有133个错误代码。
*/
```

**示例：**

```c++
#include <iostream>
#include <string.h>
#include <sys/stat.h>

int main(int argc, char* argv[]) {
    for (int i = 0; i < 150; i++) {
        std::cout << strerror(i) << std::endl;
    }
    int iret = mkdir("/home/cyyu/a/b/c", 0777);
    std::cout << "iret=" << iret << std::endl;
    std::cout << "errno=" << errno << std::endl;
    std::cout << strerror(errno) << std::endl;
}
```

## perror()

用于在控制台显示最近一次系统错误的详细信息，在实际开发中，服务程序在后台运行，通过控制台显示错误信息意义不大。（对调试程序略有帮助）

```c++
void perror(const char *s);
```

## 注意事项

- 调用库函数失败不一定会设置errno

并不是全部的库函数在调用失败时都会设置errno的值，以man手册为准（一般来说，不属于系统调用的函数不会设置errno，属于系统调用的函数才会设置errno）。

- errno不能作为调用库函数失败的标志

errno的值只有在库函数调用发生错误时才会被设置，当库函数调用成功时，errno的值不会被修改，不会主动的置为 0。

在实际开发中，判断函数执行是否成功还得靠函数的返回值，只有在返回值是失败的情况下，才需要关注errno的值。

# Linux信号

## 信号类型

信号（signal）是软件中断，是进程之间相互传递消息的一种方法，用于通知进程发生了事件，但是，不能给进程传递任何数据。

服务程序运行在后台，如果想让中止它，杀掉不是个好办法，因为进程被杀的时候，是突然死亡，没有安排善后工作。如果向服务程序发送一个信号，服务程序收到信号后，调用一个函数，在函数中编写善后的代码，程序就可以有计划的退出。如果向服务程序发送0的信号，可以检测程序是否存活。

在Shell中，可以用 `kill` 和 `killall` 命令发送信号：

```sh
kill -9 PID
killall -9 进程名
```

**信号类型：** 

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

**处理动作：**

| 处理动作 | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| A        | 缺省的动作是终止进程。                                       |
| B        | 缺省的动作是忽略此信号，将该信号丢弃，不做处理。             |
| C        | 缺省的动作是终止进程并进行内核映像转储（core dump）。        |
| D        | 缺省的动作是停止进程，进入停止状态的程序还能重新继续，一般是在调试的过程中。 |
| E        | 信号不能被捕获。                                             |
| F        | 信号不能被忽略。                                             |

## signal()

**函数声明：**

```c++
/**
 * @brief 设置信号处理方式
 * @param signum 信号值
 * @param handler 信号处理方式
 * @return 信号处理函数的返回值
 */
sighandler_t signal(int signum, sighandler_t handler);
```

**handler处理方式：**

1. `SIG_DFL`：恢复参数 `signum` 信号的处理方法为默认行为，大部分的信号的默认操作是终止进程。

2. 一个自定义的处理信号的函数，函数的形参是信号的编号。

3. `SIG_IGN`：忽略参数 `signum` 所指的信号。

**示例：** 

```c++
#include <iostream>
#include <signal.h>

void handle(int sig) {
    std::cout << "信号处理函数" << std::endl;
    exit(0);
}

int main(int argc, char* argv[]) {
    for (int i = 0; i < 64; i++) signal(i, SIG_IGN);
    signal(2, handle);
    while (true) {}
}
```

# 进程

## 进程终止

有8种方式可以中止进程，其中5种为正常终止：

1）在 `main()` 函数用 `return` 返回；

2）在任意函数中调用` exit()` 函数；

3）在任意函数中调用 `_exit()` 或 `_Exit()` 函数；

4）最后一个线程从其启动例程（线程主函数）用 `return` 返回；

5）在最后一个线程中调用 `pthread_exit()` 返回；

异常终止有3种方式：

6）调用 `abort()` 函数中止；

7）接收到一个信号；

8）最后一个线程对取消请求做出响应。

### 进程终止的状态

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

### 资源释放的问题

`retun` 表示函数返回，会调用局部对象的析构函数，`main()` 函数中的 `return` 还会调用全局对象的析构函数。

`exit()` 表示终止进程，不会调用局部对象的析构函数，只调用全局对象的析构函数。

`exit()` 会执行清理工作，然后退出，`_exit()` 和 `_Exit()` 直接退出，不会执行任何清理工作。

### atexit()

进程可以用 `atexit()` 函数登记终止函数（最多32个），这些函数将由 `exit()` 自动调用。

**函数声明：**

```c++
int atexit(void (*function)(void));
```

exit()调用终止函数的顺序与登记时相反。 

## 调用可执行程序

Linux提供了 `system()` 函数和 `exec` 函数族，在C++程序中，可以执行其它的程序（二进制文件、操作系统命令或Shell脚本）。

### system()

把需要执行的程序和参数用一个字符串传给system()函数。

**函数声明：**

```c++
/**
 * @brief 执行shell命令
 * @param string shell命令
 * @return 0-成功，非0-程序不存在或程序执行失败
 */
int system(const char * string);
```

**示例：**

```c++
#include <stdlib.h>
#include <iostream>
int main(int argc, char* argv[]) {
    if (system("ls -l /home/cyyu") != 0) {
        std::cout << "Error: system call failed" << std::endl;
    }
}
```

### exec函数族

**函数声明：**

```c++
/**
 * @brief 替换当前进程映像
 * @param path 可执行程序路径
 * @param arg 可执行程序参数
 * @return 成功不返回，失败返回-1，失败原因存于errno中
 * @note 参数arg的最后一个元素必须是NULL。
 */
int execl(const char *path, const char *arg, ...);
/**
 * @brief 替换当前进程映像
 * @param path 可执行程序路径
 * @param argv 可执行程序参数
 * @return 成功不返回，失败返回-1，失败原因存于errno中
 * @note 参数argv的最后一个元素必须是NULL。
 */
int execv(const char *path, char *const argv[]);

/**
 * @note 新进程的进程编号与原进程相同，但是，新进程取代了原进程的代码段、数据段和堆栈。
 * @note 当在主程序中成功调用exec后，被调用的程序将取代调用者程序，也就是说，exec函数之后的代码都不会被执行。
 */
```

**示例：**

```c++
#include <iostream>
#include <unistd.h>
int main(int argc, char* argv[]) {
#if 1
    if (execl("/bin/ls", "ls", "-l", NULL) == -1) {
        perror("execl");
    }
#else
    char* args[5];
    args[0] = (char*)"ls";
    args[1] = (char*)"-l";
    args[2] = NULL;
    if (execv("/bin/ls", args) == -1) {
        perror("execl");
    }
#endif
}
```

## 创建进程

### 进程标识

每个进程都有一个非负整数表示的唯一的进程ID。虽然是唯一的，但是进程ID可以复用。当一个进程终止后，其进程ID就成了复用的候选者。Linux采用延迟复用算法，让新建进程的ID不同于最近终止的进程所使用的ID。这样防止了新进程被误认为是使用了同一ID的某个已终止的进程。

```c++
/**
 * @brief 获取当前进程的ID
 * @return 当前进程的ID
 */
pid_t getpid(void); 
/**
 * @brief 获取父进程的ID
 * @return 父进程的ID
 */
pid_t getppid(void);  // 获取父进程的ID。
```

整个linux系统全部的进程是一个树形结构。

0号进程（系统进程）是所有进程的祖先，它创建了1号和2号进程。

1号进程（systemd）负责执行内核的初始化工作和进行系统配置。

2号进程（kthreadd）负责所有内核线程的调度和管理。

用pstree命令可以查看进程树（yum -y install psmisc）。

```sh
pstree -p 进程编号
```

### fork()

```c++
/**
 * @brief 创建子进程
 * @return 成功返回子进程的进程ID，失败返回-1，失败原因存于errno中
 */
pid_t fork(void);
```

由 `fork()` 创建的新进程被称为子进程。子进是父进程的副本，父进程和子进程都从调用 `fork()` 之后的代码开始执行。

fork()函数被调用一次，但返回两次。两次返回的区别是子进程的返回值是0，而父进程的返回值则是子进程的进程ID。

子进程获得了父进程数据空间、堆和栈的副本（**注意：子进程拥有的是副本，不是和父进程共享**）。

fork()之后，父进程和子进程的执行顺序是不确定的。

```c++
#include <iostream>
#include <string>
#include <unistd.h>

int main() {
    std::string str = "hello world";
    pid_t pid = fork();
    if(pid > 0){
        sleep(1);
        std::cout << "parent process   " << std::endl;
        std::cout << "parent pid:" << pid << std::endl;
        std::cout << "parent str:" << str << std::endl;
    }else if(pid == 0){
        str = "hello child";
        std::cout << "child process    " << std::endl;
        std::cout << "child pid:" << pid << std::endl;
        std::cout << "child str:" << str << std::endl;
    }
}
```

**fork()的两种用法：**

1. 父进程复制自己，然后，父进程和子进程分别执行不同的代码。这种用法在网络服务程序中很常见，父进程等待客户端的连接请求，当请求到达时，父进程调用 `fork()` ，让子进程处理些请求，而父进程则继续等待下一个连接请求。

2. 进程要执行另一个程序。这种用法在Shell中很常见，子进程从 `fork()` 返回后立即调用 `exec` 。

### 共享文件

`fork()` 的一个特性是在父进程中打开的文件描述符都会被复制到子进程中，父进程和子进程共享同一个文件偏移量。

如果父进程和子进程写同一描述符指向的文件，但又没有任何形式的同步，那么它们的输出可能会相互混合。

**示例：**

```c++
#include <fstream>
#include <iostream>
#include <unistd.h>

int main() {
    std::ofstream fout;
    fout.open("/tmp/tmp.txt");
    fork();
    for (int i = 0; i < 10000; i++)  
    {
        fout << "进程" << getpid() << "==" << i << "\n";
    }

    fout.close();
}
```

### vfork()

```c++
/**
 * @brief 创建子进程
 * @return 成功返回子进程的进程ID，失败返回-1，失败原因存于errno中
 */
pid_t vfork(void);
```

`vfork()` 函数的调用和返回值与fork()相同，但两者的语义不同。

`vfork()` 函数用于创建一个新进程，而该新进程的目的是 `exec` 一个新程序，它不复制父进程的地址空间，因为子进程会立即调用exec，于是也就不会使用父进程的地址空间。如果子进程使用了父进程的地址空间，可能会带来未知的结果。

`vfork()` 和 `fork()` 的另一个区别是：`vfork()` 保证子进程先运行，在子进程调用 `exec` 或 `exit()` 之后父进程才恢复运行。

## 僵尸进程

如果父进程比子进程先退出，子进程将被1号进程托管（这也是一种让程序在后台运行的方法）。

如果子进程比父进程先退出，而父进程没有处理子进程退出的信息，那么，子进程将成为**僵尸进程**。

**僵尸进程有什么危害**

内核为每个子进程保留了一个数据结构，包括进程编号、终止状态、使用CPU时间等。父进程如果处理了子进程退出的信息，内核就会释放这个数据结构，父进程如果没有处理子进程退出的信息，内核就不会释放这个数据结构，子进程的进程编号将一直被占用。系统可用的进程编号是有限的，如果产生了大量的僵尸进程，将因为没有可用的进程编号而导致系统不能产生新的进程。

**僵尸进程的避免：**

1）子进程退出的时候，内核会向父进程发头SIGCHLD信号，如果父进程用signal(SIGCHLD,SIG_IGN)通知内核，表示自己对子进程的退出不感兴趣，那么子进程退出后会立即释放数据结构。

2）父进程通过wait()/waitpid()等函数等待子进程结束，在子进程退出之前，父进程将被阻塞待。

```c++
/**
 * @brief 等待子进程终止
 * @param stat_loc 子进程终止的信息。（1）如果正常终止，宏WIFEXITED(stat_loc)返回真，宏WEXITSTATUS(stat_loc)可获取终止状态；（2）如果异常终止，宏WTERMSIG(stat_loc)可获取终止进程的信号。
 * @return 返回子进程的进程编号，如果调用失败返回-1，失败原因存于errno中
 */
pid_t wait(int *stat_loc);
pid_t waitpid(pid_t pid, int *stat_loc, int options);
pid_t wait3(int *status, int options, struct rusage *rusage);
pid_t wait4(pid_t pid, int *status, int options, struct rusage *rusage);
```

返回值是子进程的编号。

如果父进程很忙，可以捕获 `SIGCHLD` 信号，在信号处理函数中调用 `wait()` / `waitpid()`。

**示例1：**

```c++
#include <iostream>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
int main() {
    if (fork() > 0) {
        int   sts;
        pid_t pid = wait(&sts);
        std::cout << "已终止的子进程编号是：" << pid << std::endl;
        if (WIFEXITED(sts)) {
            std::cout << "子进程是正常退出的，退出状态是：" << WEXITSTATUS(sts) << std::endl;
        }
        else {
            std::cout << "子进程是异常退出的，终止它的信号是：" << WTERMSIG(sts) << std::endl;
        }
    }
    else { 
        int* p = 0;
        *p = 10;
        exit(1);
    }
}
```

**示例2：**

```c++
#include <iostream>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

void func(int sig)
{
    int   sts;
    pid_t pid = wait(&sts);
    std::cout << "已终止的子进程编号是：" << pid << std::endl;
    if (WIFEXITED(sts)) {
        std::cout << "子进程是正常退出的，退出状态是：" << WEXITSTATUS(sts) << std::endl;
    }
    else {
        std::cout << "子进程是异常退出的，终止它的信号是：" << WTERMSIG(sts) << std::endl;
    }
}

int main() {
    signal(SIGCHLD, func);
    if (fork() > 0) {
        while (true) {
            std::cout << "父进程忙着执行任务。\n";
            sleep(1);
        }
    }
    else {
        // sleep(5);
        int *p=0; *p=10;
        exit(1);
    }
}
```

## 多进程与信号

在多进程的服务程序中，如果子进程收到退出信号，子进程自行退出，如果父进程收到退出信号，应该先向全部的子进程发送退出信号，然后自己再退出。

**函数声明：**

```c++
/**
 * @brief 向进程发送信号
 * @param pid 进程号，当pid>0时，向进程号为pid的进程发送信号；当pid=0时，向和当前进程相同进程组的所有进程发送信号，常用于父进程给子进程发送信号；当pid=-1时，向系统内所有的进程发送信号。
 * @param sig 信号值，当sig=0时，不发送任何信号，但是可以用来检测进程是否存在，因为如果进程不存在，则返回-1，errno被设置为ESRCH。
 * @return 成功返回0，失败返回-1
 */
int kill(pid_t pid, int sig);
```

**示例：**

[code](https://github.com/cyyuz/Cpp/blob/main/src/%E6%B0%94%E8%B1%A1%E6%95%B0%E6%8D%AE%E4%B8%AD%E5%BF%83/19-6%E5%A4%9A%E8%BF%9B%E7%A8%8B%E4%B8%8E%E4%BF%A1%E5%8F%B7/demo1.cpp)

## 共享内存

多线程共享进程的地址空间，如果多个线程需要访问同一块内存，用全局变量就可以了。

在多进程中，每个进程的地址空间是独立的，不共享的，如果多个进程需要访问同一块内存，不能用全局变量，只能用共享内存。

共享内存（Shared Memory）允许多个进程（不要求进程之间有血缘关系）访问同一块内存空间，是多个进程之间共享和传递数据最高效的方式。进程可以将共享内存连接到它们自己的地址空间中，如果某个进程修改了共享内存中的数据，其它的进程读到的数据也会改变。

共享内存没有提供锁机制，也就是说，在某一个进程对共享内存进行读/写的时候，不会阻止其它进程对它的读/写。如果要对共享内存的读/写加锁，可以使用信号量。

**查看系统的共享内存：**

```sh
$ ipcs -m

------ Shared Memory Segments --------
key        shmid      owner      perms      bytes      nattch     status
0x00005005 0          cyyu       640        56         0
(键值)   (共享内存id)  (拥有者)     (权限)      (大小)  

# 删除共享内存
$ ipcrm -m 0(shmid)
```

**shmget函数声明：**

```c++
/**
 * @brief 创建/获取共享内存
 * @param key 共享内存的键值，是一个整数（unsigned int），一般采用十六进制，不同共享内存的key不能相同。
 * @param size 共享内存的大小，以字节为单位。
 * @param shmflg 共享内存的访问权限，与文件的权限一样。
 *               例如0666|IPC_CREAT，0666表示全部用户对它可读写，IPC_CREAT表示如果共享内存不存在，就创建它。
 * @return 成功返回共享内存的id（一个非负的整数），失败返回-1（系统内存不足、没有权限）
 */
int shmget(key_t key, size_t size, int shmflg);
```

**shmat函数声明：**

```c++
/**
 * @brief 把共享内存连接到当前进程的地址空间
 * @param shmid 共享内存的id，由shmget()函数返回的。
 * @param shmaddr 指定共享内存连接到当前进程中的地址位置，通常填0，表示让系统来选择共享内存的地址。
 * @param shmflg 标志位，通常填0。
 * @return 成功返回共享内存起始地址，失败返回(void*)-1。
 */
void *shmat(int shmid, const void *shmaddr, int shmflg);
```

**shmdt函数声明：**

```c++
/**
 * @brief 把共享内存从当前进程中分离
 * @param shmaddr shmat()函数返回的地址。
 * @return 成功返回0，失败返回-1。
 */
int shmdt(const void *shmaddr);
```

**shmctl函数声明：**

```c++
/**
 * @brief 操作共享内存，最常用的操作是删除共享内存。
 * @param shmid shmget()函数返回的共享内存id。
 * @param command 操作共享内存的指令，如果要删除共享内存，填IPC_RMID。
 * @param buf 操作共享内存的数据结构的地址，如果要删除共享内存，填0。
 * @return 成功返回0，失败返回-1。
 */
int shmctl(int shmid, int command, struct shmid_ds *buf);
```

> **注意**：用root创建的共享内存，不管创建的权限是什么，普通用户无法删除。

**示例：**

[code](https://github.com/cyyuz/Cpp/blob/main/src/%E6%B0%94%E8%B1%A1%E6%95%B0%E6%8D%AE%E4%B8%AD%E5%BF%83/19-7%E5%85%B1%E4%BA%AB%E5%86%85%E5%AD%98/demo1.cpp)

## 信号量

**查看系统的信号量：**

```sh
$ ipcs -s

------ Semaphore Arrays --------
key        semid      owner      perms      nsems     
0x00005005 0          cyyu       666        1    

# 删除信号量
$ ipcrm sem 0(semid)
```

**示例：**

[code](https://github.com/cyyuz/Cpp/blob/main/src/%E6%B0%94%E8%B1%A1%E6%95%B0%E6%8D%AE%E4%B8%AD%E5%BF%83/19-9%E4%BF%A1%E5%8F%B7%E9%87%8F/demo1.cpp)

# 网络编程



