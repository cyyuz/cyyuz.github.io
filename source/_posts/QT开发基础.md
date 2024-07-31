---
title: QT开发笔记
date: 2024-06-29 17:15:20
tags:
categories:
- [QT]
---

# 1 数据类型

## 1.1 输出流

```c++
#include <QDebug>
qDebug() << str;
```

用法与 std::cout 相似，自动换行。std::cout 不能直接输出 QString，需要 qPrintable 处理。QDateTime等类型 qDebug() 可以直接输出。

性能上 ` printf > std::cout >> qDebug` 。

## 1.2 Qt基本数据类型

```c++
#include <QtGlobal>
```

| 类型名称              | C类型              | 描述                                             |
| --------------------- | ------------------ | ------------------------------------------------ |
| qint8                 | signed char        | 有符号8位整形。                                  |
| qint16                | short              | 有符号16位整形。                                 |
| qint32                | int                | 有符号32位整型。                                 |
| qint64 \| qlonglong   | long long          | 有符号64位整型。                                 |
| qintptr \| qptrdiff   | qint32 \| qint64   | 指针类型，32位系统是qint32，64位系统是qint64。   |
| qreal                 | double \| float    | 除非配了-qreal float选项，否则默认为double。     |
| quint8 \| uchar       | unsigned char      | 无符号8位整形。                                  |
| quint16 \| ushort     | unsigned short     | 无符号16位整形。                                 |
| quint32 \| uint       | unsigned int       | 无符号32位整形。                                 |
| quint64 \| qulonglong | unsigned long long | 无符号64位整形。                                 |
| quintptr              | quint32 \| qint64  | 指针类型，32位系统是quint32，64位系统是quint64。 |

## 1.3 QString

| 名称        | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| +/+=        | 连接两个字符串。                                             |
| append()    | 等同于+=，追加到变量末尾。                                   |
| sprintf()   | 等同于 `sprintf()` ，返回字符串。                            |
| arg()       | 类似于 `printf()`，类型安全，支持Unicode，可以改变参数顺序。 |
| instert()   |                                                              |
| prepend()   |                                                              |
| replace()   |                                                              |
| startWith() | 是否以目标字符串开始。第二个参数 `Qt::CaseInsensitive` / `Qt::CaseSensitive` 设置大小写敏感。 |
| endsWith()  | 是否以目标字符串结尾。                                       |
| contains()  | 是否包含目标字符串。                                         |
| toInt()     | 转换为整型，第二个参数表示字符串的格式。类似有 `toDuble()` 、 `toFloat()` 、 `toLong()` 等。 |
| compare()   | 比较字符串。                                                 |
| toIUtf8()   | 转换为 `QByteArray` 类型。                                   |

- 输出字符串带有双引号，用 `qPrintable(str)` 去掉双引号。

## 1.4 QBateArray

存放的是ACCIC码。

| 名称      | 描述                       |
| --------- | -------------------------- |
| at()      | 索引，类似于vector::at()。 |
| toLower() | 字符大写转小写。           |
| toUpper() | 字符小写转大写。           |

## 1.5 QDateTime

Qt时间类型。

| 名称              | 描述                |
| ----------------- | ------------------- |
| currentDateTime() | 返回QDateTime类型。 |
| toString()        | 转换成字符串。      |

## QMap

## Qhash

## QVector

## QList

## QLinkeList

## QVariant

## 常用算法

## 正则表达式

# 2 常用开发控件

## 2.1 信号与槽机制

## Layouts
56
## Spacers

## Buttons
1:26  + 1:51
## Containers

## ItemViews
1:51
## ItemWidgets

## Input_Display
2:20

# 布局、对话框

## QLayout 

## QStacked Widget

## QSplitter

## QDockWidget

## 文件对话框

## 颜色对话框

## 字体对话框

## 输入对话框

## 消息对话框

## 自定义对话框

