---
title: ls
date: 2024-08-31 16:38:24
tags:
---

# 数据结构

## 红黑树

**红黑树用途：**

Linux内核的进程调度算法（CFS），epoll事件管理，nginx的定时器管理，redis的数据库键空间操作等等。

**红黑树性质：**

1. 每个节点是红色或黑色；
2. 根节点是黑色；
3. 每个叶子节点（NIL节点）是黑色；
4. 每个红色节点的两个子节点都是黑色；
5. 从任一节点到其每个叶子的所有路径都包含相同数目的黑色节点。

**红黑树旋转**

![旋转](../img/ls/rbtree旋转.png)

**示例：**

[code](https://github.com/cyyuz/Cpp/blob/main/src/Linux%E6%9C%8D%E5%8A%A1%E5%99%A8/01.%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84/%E7%BA%A2%E9%BB%91%E6%A0%91/rbtree.cpp)