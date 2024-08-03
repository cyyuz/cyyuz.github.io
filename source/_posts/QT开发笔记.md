---
title: QT开发笔记
date: 2024-06-29 17:15:20
tags:
categories:
- [QT]
---

# 1 软件安装

## 1.1 安装Qt

下载地址：https://download.qt.io/archive/qt/5.12/

# 2 数据类型

## 2.1 QDebug

```c++
#include <QDebug>
qDebug() << str;
```

QDebug类提供的qDebug()函数，是Qt框架中用于调试输出的工具，用法类似于std::cout。qDebug()可以自动处理换行，并且能够直接输出Qt特有的数据类型，如QString和QDateTime，而不需要额外的转换。

性能上 ` printf > std::cout >> qDebug` 。

## 2.2 基本数据类型

```c++
#include <QtGlobal>
```

| 类型名称              | C类型              | 描述                                                         |
| --------------------- | ------------------ | ------------------------------------------------------------ |
| qint8                 | signed char        | 有符号的8位整数。                                            |
| qint16                | short              | 有符号的16位整数。                                           |
| qint32                | int                | 有符号的32位整数。                                           |
| qint64 \| qlonglong   | long long          | 有符号的64位整数。                                           |
| qintptr \| qptrdiff   | qint32 \| qint64   | 指针类型，在32位系统上是qint32，在64位系统上是qint64。       |
| qreal                 | double \| float    | 浮点数，默认为double，当编译时使用-qreal float选项，则为float。 |
| quint8 \| uchar       | unsigned char      | 无符号的8位整数。                                            |
| quint16 \| ushort     | unsigned short     | 无符号的16位整数。                                           |
| quint32 \| uint       | unsigned int       | 无符号的32位整数。                                           |
| quint64 \| qulonglong | unsigned long long | 无符号的64位整数。                                           |
| quintptr              | quint32 \| qint64  | 指针类型，在32位系统上是quint32，在64位系统上是quint64。     |

## 2.3 QString

用于处理Unicode字符串的类。

| 函数名称     | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| +/+=         | 连接两个字符串。                                             |
| append()     | 等同于+=，将字符串追加到当前字符串的末尾。                   |
| sprintf()    | 类似于`sprintf()`，用于格式化字符串并返回结果。              |
| arg()        | 类似于`printf()`，提供类型安全的字符串格式化，支持Unicode，可以改变参数的顺序。 |
| insert()     | 在指定位置插入字符串。                                       |
| prepend()    | 在开头插入字符串。                                           |
| replace()    | 替换字符串中的部分内容。                                     |
| startsWith() | 是否以指定的字符串开始。第二个参数 `Qt::CaseInsensitive` / `Qt::CaseSensitive` 设置大小写敏感。 |
| endsWith()   | 是否以指定的字符串结束。                                     |
| contains()   | 是否包含指定的字符串。                                       |
| toInt()      | 转换为整数。类似的函数有`toDouble()`、`toFloat()`、`toLong()`等。 |
| compare()    | 比较两个字符串。                                             |
| toUtf8()     | 将字符串转换为`QByteArray`类型。                             |

- 当输出字符串时，如果需要去除两边的双引号，可以使用`qPrintable(str)`来实现。

## 2.4 QBateArray

用于存储原始字节数据的类，主要用于处理二进制数据。

| 函数名称  | 描述                                                |
| --------- | --------------------------------------------------- |
| at()      | 通过索引访问数组中的元素，类似于std::vector::at()。 |
| toLower() | 将数组中的字符从大写转换为小写。                    |
| toUpper() | 将数组中的字符从小写转换为大写。                    |

## 2.5 QDateTime

Qt中的时间类型，用于处理日期和时间。

| 名称                | 描述                                    |
| ------------------- | --------------------------------------- |
| `currentDateTime()` | 返回当前的日期和时间，类型为QDateTime。 |
| `toString()`        | 将QDateTime对象转换为字符串格式。       |

## 2.6 QMap、QHash

| 函数名称                      | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| `[]`                          | 插入数据或通过key获取value。                                 |
| `insert()`                    | 插入数据。                                                   |
| `remove()`                    | 删除数据。                                                   |
| `insertMulti()`               | 插入相同的key。`QMultiMap` 类型允许 key 相同。                |
| `iterator` & `const_iterator` | 迭代器。                                                     |
| `begin()` & `constBegin()`    | 返回指向第一个元素的迭代器。                                 |
| `end()` & `constEnd()`        | 返回指向最后一个元素之后的位置的迭代器。                     |
| `value()`                     | 查找key对应的value。                                         |
| `key()`                       | 查询value对应的key。                                         |
| `contains()`                  | 是否包含key。                                                |
| `keys()`                      | 返回一个 `QList` 类型的对象，包含所有key。                   |
| `values()`                    | 返回一个 `QList` 类型的对象，包含所有value。                 |

- QHash 和 QMap 的 API 几乎完全相同。

- QHash 的查找速度为 O(1)，而 QMap 的查找速度为 O(log n)。

- QMap 按 key 的顺序存储元素，QHash 使用哈希表来存储元素。

- QMap 的 key 类型必须支持 `<` 运算符。QHash 的 key 类型必须支持 `==` 运算符，和全局散列函数 `qHash()` 。

`QMapIterator` 是 `QMap` 的迭代器类型，会自动检查是否越界，操作时更安全。

| 函数名称    | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| `hasNext()` | 检查是否存在下一个元素。返回一个布尔值，如果存在下一个元素，则返回 `true`，否则返回 `false`。 |
| `next()`    | 移动到下一个元素，必须在 `hasNext()` 返回 `true` 后调用，允许通过 `key()` 和 `value()` 获取元素的键和值。 |

## 2.7 QVector

| 函数名称     | 描述                                         |
| ------------ | -------------------------------------------- |
| `<<`         | 末尾追加元素。                               |
| `append`     | 末尾追加元素。                               |
| `count()`    | 返回元素的数量。                             |
| `[]`         | 通过索引访问元素。                           |
| `remove()`   | 移除指定位置的元素，或移除特定范围内的元素。 |
| `contains()` | 是否包含某个元素，返回一个布尔值。           |

## QList

34

## QLinkedList

## QVariant

30

## 常用算法

28

## 正则表达式

# 3 常用开发控件

## 3.1 基类

MainWindow、Widget、Dialog

## 3.2 信号与槽机制


1. **定义**

**信号（Signal）**：在Qt中，信号是观察者模式，用于在程序中传递消息。信号本质是事件，当特定条件满足时，信号被触发。

**槽（Slot）**：槽是与信号关联的函数，用于响应信号。当信号被触发时，与之关联的槽函数会被自动调用，执行相应的操作。

**信号与槽机制**：将槽函数与信号关联，可以定义特定事件发生时应执行的操作。类似于Linux中的信号处理和回调函数，允许程序以解耦的方式处理事件和响应。

2. **QObject::connect**

用于实现信号和槽函数之间的关联。

```c++
QMetaObject::Connection QObject::connect(const QObject *sender, const char *signal, const QObject *receiver, const char *method, Qt::ConnectionType type = Qt::AutoConnection)
```

| 参数     | 类型           | 描述         |
| -------- | -------------- | ------------ |
| sender   | const QObject* | 信号发送者。 |
| signal   | const char*    | 信号。       |
| receiver | const QObject* | 信号接收者。 |
| method   | const char*    | 槽函数。     |

- 信号和槽的连接机制
  - 支持信号与信号之间的连接。
  - 允许一个信号连接到多个槽。
  - 允许一个槽响应多个信号。

3. **信号和槽机制特点**

提供了松散耦合的通信方式，不同组件之间的交互更加灵活，但可能会牺牲一定的性能。与直接调用非虚函数相比，通过信号调用槽函数的速度慢：

- 多线程中，信号可能需要排队等待。
- 需要编组和解组传递的参数。
- 安全地遍历所有关联的槽。
- 需要定位接收信号的对象。

为了支持信号和槽，一个类必须继承自QObject或其子类。Qt的信号和槽机制不支持模板的使用。

4. **示例代码**

dialog.h

```c++
#ifndef DIALOG_H
#define DIALOG_H

#include <QDialog>
#include <QLabel>       // 引入QLabel类，用于显示文本标签
#include <QPushButton>  // 引入QPushButton类，用于创建按钮
#include <QLineEdit>    // 引入QLineEdit类，用于创建文本编辑框

// Dialog类继承自QDialog，用于创建一个对话框界面
class Dialog : public QDialog
{
    Q_OBJECT

public:
    Dialog(QWidget *parent = nullptr);
    ~Dialog();

private:
    QLabel *label1, *label2;  // 用于显示文本的标签
    QPushButton *pushButton;  // 用于触发事件的按钮
    QLineEdit *lineEdit;      // 用于输入文本的编辑框

private slots:
    void CalculateSphereVolume();  // 私有槽函数，用于计算球体体积
};
```

dialog.cpp

```c++
#include "dialog.h"

#include <QGridLayout> // 引入QGridLayout类，用于创建网格布局

const static double PI = 3.1415;

// 构造函数实现
Dialog::Dialog(QWidget *parent)
    : QDialog(parent)  
{
    // 创建标签，用于提示用户输入
    label1 = new QLabel(this);  
    label1->setText(tr("请输入球体半径："));
        
    // 创建标签，用于显示计算结果
    label2 = new QLabel(this);  
	
    // 创建按钮，用于触发计算体积的操作
    pushButton = new QPushButton(this);  
    pushButton->setText(tr("计算球体体积"));
	
    // 创建编辑框，用于用户输入球体半径
    lineEdit = new QLineEdit(this);  
	
    // 创建并设置网格布局
    QGridLayout *gridLayout = new QGridLayout(this);  
    gridLayout->addWidget(label1, 0, 0);
    gridLayout->addWidget(label2, 1, 0);
    gridLayout->addWidget(lineEdit, 0, 1);  
    gridLayout->addWidget(pushButton, 1, 1); 
        
	// 关联信号和槽
    connect(pushButton, SIGNAL(clicked()), this, SLOT(CalculateSphereVolume()));  
}

Dialog::~Dialog()
{
}

void Dialog::CalculateSphereVolume(){
    bool isLoop;
    QString tmpStr;
    int radius = lineEdit->text().toInt(&isLoop);  // 从编辑框获取半径值，并转换为整数
    double volume = 4.0 / 3.0 * PI * radius * radius * radius;  // 计算球体体积   
    label2->setText(tmpStr.setNum(volume));  // 将计算结果设置为label2的文本
}
```

main.cpp

```c++
#include "dialog.h"

#include <QApplication> 

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    Dialog w;

    w.setWindowTitle("计算球体体积");  // 设置窗口标题

    w.show();
    return a.exec();
}
```

5. **构造函数参数 `this`**

将`this`作为构造函数参数传递给控件，作用是指定控件的父对象，有以下作用：

1. **内存管理**：在Qt中，控件通常会自动删除其子控件。将`this`作为父对象传递给控件时，当父控件（`Dialog`）被删除时，所有子控件也会被自动删除。这样可以简化内存管理，避免内存泄漏。
2. **事件传递**：在Qt中，事件（如鼠标点击、键盘输入等）会从父控件传递到子控件。通过指定父对象，可以控制事件传递的层次结构。
3. **布局管理**：在Qt中，布局管理器（如`QGridLayout`）会自动调整控件的大小和位置。将控件添加到布局时，布局管理器会根据控件的父对象来调整它们。通过将`this`作为父对象，可以确保控件被正确地添加到对话框的布局中。

6. **`tr()`**

使用`tr()`函数，将文本标记为可翻译的，在应用程序中支持多语言。

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

# 疑问

MainWindow、Widget、Dialog的区别 

信号 观察者模式