---
title: C++新特性
date: 2024-09-03 19:24:59
tags: 
categories:
- [技术, cpp]
index_img: img/C++/C++11.jpg
---

# 类型推导

- auto

auto 关键字使用已声明变量的初始化表达式或 lambda 表达式参数来推导其类型。

语法：`auto 变量 = 表达式`

```c++
// 初始化
auto a {42};
auto b = 42;
auto c = "123";  // const char *
```

auto 关键字是类型的占位符，本身不是类型。 因此，auto 关键字不能用于强制转换或运算符，如 sizeof 和typeid。

- decltype

`decltype(表达式) 变量`

```c++
decltype(123) a;    // int
decltype("123") b = "456";  // char const [4]
```

# 范围for循环

适用于所有支持 `begin()` 和 `end()` 的函数，或者原生数组。

```c++
// std::initializer_list<int>
for (auto a : {1, 2, 3, 4}) {   
    std::cout << a << std::endl;
}
```

# lambda表达式

lambda 表达式用于定义并创建匿名函数对象，它可以捕获其所在作用域中的变量，并可以在其作用域内执行。

语法：`[捕获列表](参数列表) mutable(可选) 异常属性 -> 返回类型 {函数体}`

```c++
#include <algorithm>

std::vector<int> v1 = { 7,3,8,5,1 };
sort(v1.begin(), v1.end(), [](int a, int b) -> bool {return a < b; });

auto func = [](int a, int b) -> bool {
    return a < b;
};
std::cout << typeid(func).name() << std::endl;   // class `int __cdecl main(void)'::`2'::<lambda_1>
```

# 智能指针

智能指针是封装了原生指针的类，自动管理动态内存，防止内存泄漏和其他与手动管理内存相关的错误。C++11 提供了三种标准的智能指针类型：std::unique_ptr、std::shared_ptr 和 std::weak_ptr。

头文件： `<memory>`

- **unique_ptr**

`unique_ptr` 独占所有权的智能指针，同一时间只能有一个 `unique_ptr` 指向特定内存。不能复制到其他 `unique_ptr`，不能通过值传递到函数，只能移动 `unique_ptr`，内存资源所有权将转移到另一个 `unique_ptr`，原来的 `unique_ptr` 不再拥有此资源。 

当 `unique_ptr` 超出作用域时，会自动删除所管理的对象。

```cpp
// 初始化
std::unique_ptr<int> ptr3 = std::make_unique<int>(10); // 推荐
std::unique_ptr<int> ptr1(new int(10));

int* a = new int(10);
std::unique_ptr<int> ptr2(a); // 错误初始化，当ptr2释放，a是一个野指针

// move转移所有权
std::unique_ptr<int> ptr4 = std::move(ptr3);
if(ptr3) // 是否为空

// reset重置指向对象
ptr3.reset(net int<10>);

// 显示释放内存
ptr1.reset();

// release释放控制权，返回原生指针
int* b = ptr4.release();
```

- **shared_ptr**

共享所有权的智能指针，多个 `shared_ptr` 可以指向同一内存，内存在最后一个 `shared_ptr` 被销毁时释放。

`shared_ptr` 初始化一个 shared_ptr 之后，按值将其传入函数参数，然后将其分配给其他 shared_ptr 实例。 所有实例均指向同一个对象，并共享对一个“控制块”（每当新的 shared_ptr 添加、超出范围或重置时增加和减少引用计数）的访问权限。 当引用计数达到零时，控制块将删除内存资源和自身。

shared_ptr是共享所有权的智能指针，它允许多个智能指针共享同一个对象，当最后一个shared_ptr被销毁时，对象才会被销毁。

```cpp
#include <iostream>
#include <memory>

class MyClass {
public:
    void doSomething() {
        std::cout << "Doing something" << std::endl;
    }
};

int main() {
    std::shared_ptr<MyClass> myPtr1(new MyClass());
    std::shared_ptr<MyClass> myPtr2 = myPtr1;

    myPtr1->doSomething(); // 使用 myPtr1 调用成员函数
    myPtr2->doSomething(); // 使用 myPtr2 调用成员函数

    // 当 myPtr1 和 myPtr2 都被销毁时，MyClass 对象的内存才会被释放
    return 0;
}
```

- **weak_ptr**

weak_ptr是弱引用的智能指针，它不拥有对象的所有权，也不阻止对象被销毁，但它可以观察对象的生命周期，并在对象被销毁时自动变为空。

弱引用智能指针，用于与 `shared_ptr` 配合使用，避免循环引用导致的内存泄漏。

```cpp
#include <iostream>
#include <memory>

class Node {
public:
    std::shared_ptr<Node> next;
    std::weak_ptr<Node> prev;

    Node() : next(nullptr), prev() {}
};

int main() {
    std::shared_ptr<Node> node1 = std::make_shared<Node>();
    std::shared_ptr<Node> node2 = std::make_shared<Node>();

    node1->next = node2;
    node2->prev = node1;

    // 循环引用，但使用 weak_ptr 避免了内存泄漏
    return 0;
}
```

# function和bind

头文件： `<functional>`

- **function**

`std::function` 是一个通用的、多态的函数封装，可以存储、复制和调用任何可调用目标（函数、lambda 表达式、bind 表达式、函数对象等），并具有与存储的可调用目标相同的调用签名。

```cpp
#include <iostream>
#include <functional>

void foo(int x) {
    std::cout << "foo: " << x << std::endl;
}

int main() {
    std::function<void(int)> func = foo; // 将函数 foo 绑定到 func
    func(10); // 调用 func，实际上调用 foo

    return 0;
}
```

- **bind**

`std::bind` 是一个函数适配器，它接受一个可调用对象（如函数、函数指针、成员函数指针或 lambda 表达式）以及一些参数，并返回一个新的可调用对象，该对象在调用时将使用提供的参数调用原始可调用对象。

```cpp
#include <iostream>
#include <functional>

void foo(int x, double y) {
    std::cout << "foo: " << x << ", " << y << std::endl;
}

int main() {
    auto func = std::bind(foo, 10, std::placeholders::_1); // 将 10 绑定到第一个参数，将第二个参数作为占位符
    func(3.14); // 调用 func，实际上调用 foo(10, 3.14)

    return 0;
    }
```