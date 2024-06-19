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
        <td>dd</td>
        <td> 剪切光标所在行 </td>
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


# scp


# 