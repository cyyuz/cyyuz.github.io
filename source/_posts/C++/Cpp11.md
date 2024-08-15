---
title: C++11
date: 2024-08-14 10:20:48
tags:
categories:
- [技术, cpp]
index_img: img/C++/C++11.jpg
---

# auto & decltype

auto &

```cpp
auto &a = b;
```

auto &a = b;  a是b的引用，a的类型是b的类型。

decltype

```cpp
decltype(b) a = b;
```

decltype(a) a = b;  a的类型是b的类型，a的值是b的值。

# 智能指针

## unique_ptr

unique_ptr是独占所有权的智能指针，它不允许其他的智能指针共享其所有权，也不允许所有权转移，但允许所有权释放。

```cpp
std::unique_ptr<int> p1(new int(10)); // 创建一个指向int类型的unique_ptr，并初始化为10
std::unique_ptr<int> p2 = std::move(p1); // 将p1的所有权转移给p2
```

## shared_ptr

shared_ptr是共享所有权的智能指针，它允许多个智能指针共享同一个对象，当最后一个shared_ptr被销毁时，对象才会被销毁。

```cpp
std::shared_ptr<int> p1(new int(10)); // 创建一个指向int类型的shared_ptr，并初始化为10
std::shared_ptr<int> p2 = p1; // p2和p1共享同一个对象
```

## weak_ptr

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

## 智能指针的创建

```cpp
std::unique_ptr<int> p1(new int(10)); // 创建一个指向int类型的unique_ptr，并初始化为10
std::shared_ptr<int> p2 = std::make_shared<int>(10); // 创建一个指向int类型的shared_ptr，并初始化为10
std::weak_ptr<int> p3 = std::make_shared<int>(10); // 创建一个指向int类型的weak_ptr，并初始化为10
```

## 智能指针的销毁

智能指针在超出作用域时会自动销毁，它会释放所指向的对象，并调用对象的析构函数。

## 智能指针的拷贝和赋值

unique_ptr不允许拷贝和赋值，但允许移动。shared_ptr允许拷贝和赋值，但拷贝和赋值会导致引用计数增加。weak_ptr不允许拷贝和赋值，但可以观察对象的生命周期。

## 智能指针的访问

unique_ptr和shared_ptr可以通过解引用操作符访问所指向的对象，weak_ptr可以通过lock()函数访问所指向的对象。

## 智能指针的释放

unique_ptr和shared_ptr可以通过reset()函数释放所指向的对象，weak_ptr可以通过reset()函数释放所指向的对象，但weak_ptr不会影响对象的引用计数。

## 智能指针的引用计数

shared_ptr通过引用计数来管理对象的生命周期，当引用计数为0时，对象会被销毁。weak_ptr不参与引用计数，它只是观察对象的生命周期。

## 智能指针的异常安全

智能指针在异常发生时，会自动释放所指向的对象，从而保证异常安全。