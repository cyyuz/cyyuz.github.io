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
        <td rowspan="6"> 剪切</td>
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
# man

**1-用户命令**；2-系统接口；**3-库函数**；4-特殊文件，比如设备文件；5-文件；

6-游戏；7-系统的软件包；8-系统管理命令；9-内核。

# 编译

## gcc/g++

```shell
gcc/g++ [选项] source1.cpp source2.cpp
```

| 选项       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| -o         | 指定输出的文件名，这个名称不能和源文件同名。默认为a.out。    |
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

## makefile

## gdb

## main函数参数

# Linux时间操作

# Linux文件操作


# scp


# 