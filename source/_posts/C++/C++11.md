---
title: C++11
date: 2024-08-14 10:20:48
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

`unique_ptr` 是独占所有权的智能指针，表示某个资源（如动态分配的内存）只能有一个 std::unique_ptr 拥有，不允许其他的智能指针共享其所有权。无法复制到其他 `unique_ptr`，无法通过值传递到函数，也无法用于需要副本的任何 C++ 标准库算法。 只能移动 `unique_ptr`，内存资源所有权将转移到另一 `unique_ptr`，并且原始 `unique_ptr` 不再拥有此资源。 

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

`shared_ptr` 初始化一个 shared_ptr 之后，您可复制它，按值将其传入函数参数，然后将其分配给其他 shared_ptr 实例。 所有实例均指向同一个对象，并共享对一个“控制块”（每当新的 shared_ptr 添加、超出范围或重置时增加和减少引用计数）的访问权限。 当引用计数达到零时，控制块将删除内存资源和自身。

shared_ptr是共享所有权的智能指针，它允许多个智能指针共享同一个对象，当最后一个shared_ptr被销毁时，对象才会被销毁。

```cpp
std::shared_ptr<int> p1(new int(10)); // 创建一个指向int类型的shared_ptr，并初始化为10
std::shared_ptr<int> p2 = p1; // p2和p1共享同一个对象
```

- **weak_ptr**

weak_ptr是弱引用的智能指针，它不拥有对象的所有权，也不阻止对象被销毁，但它可以观察对象的生命周期，并在对象被销毁时自动变为空。

```cpp
std::weak_ptr<int> p1; // 创建一个空的weak_ptr
std::shared_ptr<int> p2(new int(10)); // 创建一个指向int类型的shared_ptr，并初始化为10

p1 = p2; // p1和p2共享同一个对象
if (p1.expired()) { // 检查p1是否已经过期
    std::cout << "p1 has expired" << std::endl;
} else {
    std::cout << "p1 is valid" << std::endl;
}
```