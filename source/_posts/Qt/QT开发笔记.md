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

| 函数            | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| `+/+=`          | 连接两个字符串。                                             |
| `append()`      | 等同于+=，将字符串追加到当前字符串的末尾。                   |
| `sprintf()`     | 类似于`sprintf()`，用于格式化字符串并返回结果。              |
| `arg()`         | 类似于`printf()`，提供类型安全的字符串格式化，支持Unicode，可以改变参数的顺序。 |
| `insert()`      | 在指定位置插入字符串。                                       |
| `prepend()`     | 在开头插入字符串。                                           |
| `replace()`     | 替换字符串中的部分内容。                                     |
| `startsWith()`  | 是否以指定的字符串开始。第二个参数 `Qt::CaseInsensitive` / `Qt::CaseSensitive` 设置大小写敏感。 |
| `endsWith()`    | 是否以指定的字符串结束。                                     |
| `contains()`    | 是否包含指定的字符串。                                       |
| `toInt()`       | 转换为整数。类似的函数有 `toDouble()`、`toFloat()`、`toLong() `等。 |
| `compare()`     | 比较两个字符串。                                             |
| `toUtf8()`      | 将字符串转换为 `QByteArray` 类型。                           |
| `toStdString()` | 转换为 `std::string` 。                                      |

- 当输出字符串时，如果需要去除两边的双引号，可以使用`qPrintable(str)`来实现。

## 2.4 QByteArray

用于存储原始字节数据的类，主要用于处理二进制数据。

| 函数        | 描述                                                |
| ----------- | --------------------------------------------------- |
| `at()`      | 通过索引访问数组中的元素，类似于std::vector::at()。 |
| `toLower()` | 将数组中的字符从大写转换为小写。                    |
| `toUpper()` | 将数组中的字符从小写转换为大写。                    |

## 2.5 QDateTime

Qt中的时间类型，用于处理日期和时间。

| 名称                | 描述                                    |
| ------------------- | --------------------------------------- |
| `currentDateTime()` | 返回当前的日期和时间，类型为QDateTime。 |
| `toString()`        | 将QDateTime对象转换为字符串格式。       |

## 2.6 QMap、QHash

| 函数            | 描述                                           |
| --------------- | ---------------------------------------------- |
| `[]`            | 插入数据或通过key获取value。                   |
| `insert()`      | 插入数据。                                     |
| `remove()`      | 删除数据。                                     |
| `insertMulti()` | 插入相同的key。`QMultiMap` 类型允许 key 相同。 |
| `value()`       | 查找key对应的value。                           |
| `key()`         | 查询value对应的key。                           |
| `contains()`    | 是否包含key。                                  |
| `keys()`        | 返回一个 `QList` 类型的对象，包含所有key。     |
| `values()`      | 返回一个 `QList` 类型的对象，包含所有value。   |

- QHash 和 QMap 的 API 几乎完全相同。

- QHash 的查找速度为 O(1)，而 QMap 的查找速度为 O(log n)。

- QMap 按 key 的顺序存储元素，QHash 使用哈希表来存储元素。

- QMap 的 key 类型必须支持 `<` 运算符。QHash 的 key 类型必须支持 `==` 运算符，和全局散列函数 `qHash()` 。

## 2.7 QVector

| 函数         | 描述                                         |
| ------------ | -------------------------------------------- |
| `<<`         | 末尾追加元素。                               |
| `append`     | 末尾追加元素。                               |
| `count()`    | 返回元素的数量。                             |
| `[]`         | 通过索引访问元素。                           |
| `remove()`   | 移除指定位置的元素，或移除特定范围内的元素。 |
| `contains()` | 是否包含某个元素，返回一个布尔值。           |

## 2.8 QList、QLinkedList

**QList**

如果 `T` 是一个指针类型或指针大小的基本类型，`QList<T>` 将数值直接存储在数组中。否则，将存储对象的指针，指针指向相应的对象。

| 函数            | 描述                       |
| --------------- | -------------------------- |
| `insert()`      | 插入数据到指定位置。       |
| `append()`      | 添加数据到列表末尾。       |
| `at()`          | 通过索引访问元素。         |
| `contains()`    | 检查列表是否包含特定元素。 |
| `replace()`     | 替换指定位置的元素。       |
| `removeAt()`    | 删除指定索引位置的元素。   |
| `removeFirst()` | 删除列表中的第一个元素。   |

**QLinkedList**

QLinkedList 是一个双向链表，不支持通过索引访问元素，但在插入和删除操作上具有更高的效率，特别是在操作大型数据集时。

| 函数 | 描述               |
| ---- | ------------------ |
| `<<` | 向链表中插入元素。 |

## 2.9 QVariant

`QVariant` 本质为C++ `union` 数据类型，可以保存很多Qt类型的值。

**常用成员函数：**

| 函数              | 描述                                                         |
| ----------------- | ------------------------------------------------------------ |
| `type()`          | 返回当前 `QVariant` 对象中存储的数据类型。                   |
| `canConvert()`    | 检查 `QVariant` 对象是否可以转换为指定的数据类型。           |
| `value()`         | 返回 `QVariant` 对象中存储的值，需要显式指定返回值的类型。   |
| `qvariant_cast()` | 用于将 `QVariant` 对象转换为指定类型，类似于 `dynamic_cast`。 |

**常用枚举类型：**

| 变量                   | 类型           |
| ---------------------- | -------------- |
| `QVariant::Invalid`    | 无效类型       |
| `QVariant::Time`       | `QTime`        |
| `QVariant::Region`     | `QRegion`      |
| `QVariant::Line`       | `QLine`        |
| `QVariant::Palette`    | `QPalette`     |
| `QVariant::Bitmap`     | `QBitmap`      |
| `QVariant::Bool`       | `bool`         |
| `QVariant::List`       | `QList`        |
| `QVariant::Brush`      | `QBrush`       |
| `QVariant::SizePolicy` | `QSizePolicy`  |
| `QVariant::Size`       | `QSize`        |
| `QVariant::String`     | `QString`      |
| `QVariant::Char`       | `QChar`        |
| `QVariant::Map`        | `QMap`         |
| `QVariant::Color`      | `QColor`       |
| `QVariant::StringList` | `QStringList`  |
| `QVariant::Cursor`     | `QCusor`       |
| `QVariant::Point`      | `QPoint`       |
| `QVariant::Date`       | `QDate`        |
| `QVariant::Pen`        | `QPen`         |
| `QVariant::DateTime`   | `QDateTime`    |
| `QVariant::Pixmap`     | `QPixamp`      |
| `QVariant::Double`     | `double`       |
| `QVariant::Rect`       | `QRect`        |
| `QVariant::Font`       | `QFont`        |
| `QVariant::Image`      | `QImage`       |
| `QVariant::Icon`       | `QIcon`        |
| `QVariant::UserType`   | 用户自定义类型 |

## 2.10 迭代器

1. **c++风格**

Qt 容器类型如 `QString`、`QByteArray`、`QMap`、`QHash`、`QVector`、`QList`、`QLinkedList` 等支持 C++ 风格的迭代器。

- 读写迭代器

| 函数       | 描述                                         |
| ---------- | -------------------------------------------- |
| `iterator` | 迭代器。                                     |
| `begin()`  | 返回指向容器中第一个元素的迭代器。           |
| `end()`    | 返回指向容器中最后一个元素之后位置的迭代器。 |
| `++`       | 向前移动迭代器到下一个元素。                 |

- 只读迭代器

| 函数             | 描述                                             |
| ---------------- | ------------------------------------------------ |
| `const_iterator` | 迭代器，只能读取元素。                           |
| `constBegin()`   | 返回指向容器中第一个元素的只读迭代器。           |
| `constEnd()`     | 返回指向容器中最后一个元素之后位置的只读迭代器。 |

2. **java风格**

`QMapIterator`、`QHashIterator`、`QVectorIterator`、 `QListMapIterator` 等类型，会自动检查是否越界，操作时更安全。

| 函数名称    | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| `hasNext()` | 检查是否存在下一个元素。返回一个布尔值，如果存在下一个元素，则返回 `true`，否则返回 `false`。 |
| `next()`    | 移动到下一个元素，必须在 `hasNext()` 返回 `true` 后调用。    |

## 2.11 常用算法

| 函数          | 描述                                  |
| ------------- | ------------------------------------- |
| `qAbs(x)`     | 返回参数 `x` 的绝对值。               |
| `qMax(x, y)`  | 返回参数 `x` 和 `y` 中的最大值。      |
| `qRound(x)`   | 将浮点数 `x` 四舍五入到最接近的整数。 |
| `qSwap(x, y)` | 交换参数 `x` 和 `y` 的值。            |

## 2.12 正则表达式

正则表达式使用单个字符串来描述、匹配一系列匹配某个语法规则的字符串，通常被用来检索、替换那些符合某个（规则）的文本。正则表达式描述一种字符串匹配的模式（pattern），可以用来检查一个串是否含有某种子串、将匹配的子串替换成或者从某个串中取出符合某个条件的子串等。

正则表达式由表达式(expressions)、量词(quantifiers)、断言(assertions)组成。 

- 最简单的表达式是一个字符。字符集可以用表达式如"[AEIOU]",表示匹配所有的大写字母；使用"^[AEIOU]",表示匹配所有非元音字母,即辅音字母;连续的字符集可以使用表达式如"a-z",表示匹配所有的小写英文字 母。
- 量词说明表达式的出现次数，如'x{1,2}'表示 'x' 可以至少有一个，至多有两个。

**示例代码：**

```c++
#include <regex>

QString number = "12345678901";
std::regex re("^1(3|5|8)\\d{9}$");
bool result = std::regex_match(number.toStdString(), re);
```

**正则表达式的量词：**  

| 量词   | 含义                     |
| ------ | ------------------------ |
| E?     | 匹配0次或1次             |
| E+     | 匹配1次或多次            |
| E*     | 匹配0次或多次            |
| E[n]   | 匹配n次                  |
| E[,m]  | 最多匹配m次              |
| E[n,]  | 至少匹配n次              |
| E[n,m] | 至少匹配n次，最多匹配m次 |

**正则表达式的断言：**

| 符号  | 含义                      |
| ----- | ------------------------- |
| ^     | 表示在字符串开头进行匹配  |
| $     | 表示在字符串结尾进行匹配  |
| \b    | 单词边界                  |
| \B    | 非单词边界                |
| (?=E) | 表示表达式后紧随E才匹配   |
| (?!E) | 表示表达式后不跟随E才匹配 |

**正则表达式规则：**

| 字符          | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| `\`           | 将下一个字符标记为一个特殊字符、或一个原义字符、或一个向后引用、或一个八进制转义符。例如，`'n'` 匹配字符 "n"。`'\n'` 匹配换行。序列 `'\\'` 匹配 `'\'` 而 `'\('` 匹配 `'('`。 |
| `^`           | 匹配输入字符串的开始位置。如果设置了 RegExp 对象的 Multiline 属性，`^` 也匹配 `'\n'` 或 `'\r'` 之后的位置。 |
| `$`           | 匹配输入字符串的结束位置。如果设置了 RegExp 对象的 Multiline 属性，`$` 也匹配 `'\n'` 或 `'\r'` 之前的位 置。 |
| `*`           | 匹配前面的子表达式零次或多次。例如，`zo*` 能匹配 "z" 以及 "zoo"。`*` 等价于 `{0,}`。 |
| `+`           | 匹配前面的子表达式一次或多次。例如，`'zo+'` 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。`+` 等价于 `{1,}`。 |
| `?`           | 匹配前面的子表达式零次或一次。例如，`do(es)?` 可以匹配 "do" 或 "does" 中的 "do"。`?` 等价于 `{0,1}`。 |
| `{n}`         | `n` 是一个非负整数。匹配确定的 `n` 次。例如，`o{2}` 不能匹配 "Bob" 中的 o，但是能匹配 "food" 中的两个 o。 |
| `{n,}`        | `n` 是一个非负整数。至少匹配 `n` 次。例如，`o{2,}` 不能匹配 "Bob" 中的 o,但能匹配 "foooooood" 中的所有 o。`o{1,}?` 等价于 `o+`。 |
| `{n,m}`       | `n` 是一个非负整数，`m` 是一个正整数。至少匹配 `n` 次，但不超过 `m` 次。例如，`o{1,3}` 不能匹配 "Bob" 中的 o,但能匹配 "foooooood" 中的前三个 o。 |
| `?`           | 使前面的子表达式变为非贪婪模式，即尽可能少地匹配。例如，`o+?` 能匹配 "foooooood" 中的一个 o。 |
| `.`           | 匹配除换行符以外的任意字符。                                 |
| `(pattern)`   | 匹配 `pattern` 并捕获该匹配的子表达式，可以用于后面的引用。  |
| `(?:pattern)` | 匹配 `pattern` 但不捕获该匹配的子表达式。                    |
| `(?=pattern)` | 正向前瞻，匹配位于 `pattern` 之前的字符串，但不包括 `pattern`。 |
| `(?!pattern)` | 负向前瞻，匹配不位于 `pattern` 之前的字符串。                |
| `x|y`         | 匹配 `x` 或 `y`。                                            |
| `[xyz]`       | 字符集，匹配包含的任意一个字符。                             |
| `[^xyz]`      | 反向字符集，匹配不在字符集中的任意字符。                     |
| `[a-z]`       | 字符范围，匹配指定范围内的任意字符。                         |
| `[^a-z]`      | 反向字符范围，匹配不在指定范围内的任意字符。                 |
| `\b`          | 匹配一个单词边界，即字与空格之间的位置。                     |
| `\B`          | 匹配非单词边界。                                             |
| `\cx`         | 匹配由 `x` 指定的控制字符。                                  |
| `\d`          | 匹配一个数字字符。等价于 `[0-9]`。                           |
| `\D`          | 匹配一个非数字字符。等价于 `[^0-9]`。                        |
| `\f`          | 匹配一个换页符。                                             |
| `\n`          | 匹配一个换行符。                                             |
| `\r`          | 匹配一个回车符。                                             |
| `\s`          | 匹配任何空白字符，包括空格、制表符、换页符等。               |
| `\S`          | 匹配任何非空白字符。                                         |
| `\t`          | 匹配一个制表符。                                             |
| `\v`          | 匹配一个垂直制表符。                                         |
| `\w`          | 匹配包括下划线的任何单词字符。等价于 `[A-Za-z0-9_]`。        |
| `\W`          | 匹配任何非单词字符。等价于 `[^A-Za-z0-9_]`。                 |
| `\xn`         | 匹配 `n`，其中 `n` 是一个十六进制转义值。                    |
| `\num`        | 匹配 `num` 对应的八进制字符。                                |
| `\n`          | 匹配一个换行符。                                             |
| `\nm`         | 匹配 `nm` 对应的八进制字符。                                 |
| `\nml`        | 匹配 `nml` 对应的八进制字符。                                |
| `\un`         | 匹配 `n` 对应的 Unicode 字符，其中 `n` 是一个四位十六进制数。 |
| `(?=E)`       | 正向前瞻，匹配位于 `E` 之前的字符串，但不包括 `E`。          |
| `(?!E)`       | 负向前瞻，匹配不位于 `E` 之前的字符串。                      |

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

## 3.3 Layouts & Spacers

**布局控件：**

| 控件名称          | 描述       |
| ----------------- | ---------- |
| Vertical Layout   | 垂直布局。 |
| Horizontal Layout | 水平布局。 |
| Grid Layout       | 栅格布局。 |
| Form              | 表单布局。 |
| Vertical Spacers  | 垂直间隔。 |
| Horizontal Layout | 水平间隔。 |

**栅格布局示例代码：**

widget.h

```c++
#ifndef WIDGET_H
#define WIDGET_H

#include <QWidget>
#include <QGridLayout>   // 栅格控件
#include <QPushButton>   // 按钮控件

class Widget : public QWidget
{
    Q_OBJECT

public:
    Widget(QWidget *parent = nullptr);
    ~Widget();

    QGridLayout *gridLayout;
    QPushButton *button1, *button2, *button3, *button4;
};
#endif // WIDGET_H
```

widget.cpp

```c++
#include "widget.h"

Widget::Widget(QWidget *parent)
    : QWidget(parent)
{
    button1 = new QPushButton(this);
    button1->setText("aaa");
    button1->setFixedHeight(40);
    button1->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);

    button2 = new QPushButton(this);
    button2->setText("bbb");
    button2->setFixedWidth(100);
    button2->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);

    button3 = new QPushButton(this);
    button3->setText("ccc");
    button3->setFixedHeight(40);
    button3->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);

    button4 = new QPushButton(this);
    button4->setText("ddd");
    button4->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);


    gridLayout = new QGridLayout();
	gridLayout->setContentsMargins(10, 10, 10, 10); // 设置四周的边距
    gridLayout->setSpacing(20); // 设置控件之间的间距，水平和垂直

    // 将按钮添加到栅格布局中
    gridLayout->addWidget(button1, 0, 1);
    gridLayout->addWidget(button2, 0, 0, 3, 1); // 从0,0位置开始，占3行1列
    gridLayout->addWidget(button3, 2, 1);
    gridLayout->addWidget(button4, 1, 1);

    setLayout(gridLayout); // 设置为主布局
}
```

**表单布局示例代码：**

```c++
#include "widget.h"
#include <QFormLayout>
#include <QLineEdit>

Widget::Widget(QWidget *parent)
    : QWidget(parent)
{
    setFixedSize(200, 100); // 设置窗口固定大小
    setWindowTitle("表单布局测试"); // 设置窗口标题

    QFormLayout *formLayout = new QFormLayout(this);

    QLineEdit *lineEdit1 = new QLineEdit(this);
    QLineEdit *lineEdit2 = new QLineEdit(this);

    formLayout->addRow("学号", lineEdit1);
    formLayout->addRow("姓名", lineEdit2);

    formLayout->setSpacing(10); // 设置布局中的控件间距

    // 设置标签和编辑框的布局策略
    // formLayout->setRowWrapPolicy(QFormLayout::WrapAllRows); // 标签显示在编辑框上方
    formLayout->setRowWrapPolicy(QFormLayout::WrapLongRows); // 标签和编辑框在同一行

    // 设置标签的对齐方式
    formLayout->setLabelAlignment(Qt::AlignLeft); // 标签左对齐
}
```

## 3.4 Buttons

**Buttons控件：**

| 控件名称            | 描述           |
| ------------------- | -------------- |
| Push Button         | 命令按钮。     |
| Tool Button         | 工具按钮。     |
| Radio Button        | 单选按钮。     |
| Check Box           | 复选框按钮。   |
| Command Link Button | 命令链接按钮。 |
| Dialog  Button Box  | 按钮盒。       |

1. **Push Button**

mainwindow.h

```c++
#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include <QPushButton>

class MainWindow : public QMainWindow
{
    Q_OBJECT
public:
    MainWindow(QWidget *parent = nullptr);
    ~MainWindow();
private:
    QPushButton *pushButton1, *pushButton2;
private slots:
    void PushButtonClicked1();
    void PushButtonClicked2();
};
#endif // MAINWINDOW_H
```

mainwindow.cpp

```c++
#include "mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
{
    // 设置窗口位置和大小
    this->setGeometry(600,600,300,300);   
    pushButton1 = new QPushButton("命令按钮1", this);
    pushButton2 = new QPushButton("命令按钮2", this);
	
    // 设置命令按钮位置和大小
    pushButton1->setGeometry(20,20,100,30);   	
    pushButton2->setGeometry(20,60,100,30);

    connect(pushButton1, SIGNAL(clicked()), this, SLOT(PushButtonClicked1()));
    connect(pushButton2, SIGNAL(clicked()), this, SLOT(PushButtonClicked2()));
}

void MainWindow::PushButtonClicked1(){
    this->setStyleSheet("QMainWindow {background-color:rgba(255, 255, 0, 100%);}");  // 设置窗口样式
}

void MainWindow::PushButtonClicked2(){
    this->setStyleSheet("QMainWindow {background-color:rgba(255, 0, 0, 100%);}");
}
```

2. **Tool Button**







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