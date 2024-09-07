---
title: ls
date: 2024-08-31 16:38:24
tags:
---

# 数据结构

## 红黑树

[code](https://github.com/cyyuz/Cpp/blob/main/src/Linux%E6%9C%8D%E5%8A%A1%E5%99%A8/01.%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84/%E7%BA%A2%E9%BB%91%E6%A0%91/rbtree.cpp)

**红黑树用途：**

Linux内核的进程调度算法（CFS），epoll事件管理，nginx的定时器管理，redis的数据库键空间操作等等。

**红黑树性质：**

1. 每个节点是红色或黑色；
2. 根节点是黑色；
3. 每个叶子节点（NIL节点）是黑色；
4. 每个红色节点的两个子节点都是黑色；
5. 从任一节点到其每个叶子的所有路径都包含相同数目的黑色节点。

**红黑树旋转**

左旋时，x的父节点有3种情况：
1. x是root节点，即父节点为nil；
2. x是父节点的左子树；
3. x是父节点的右子树。

![旋转](../img/ls/rbtree旋转.png)

**插入节点**

步骤：

1. 二叉树查找。

2. 插入节点：（1）根节点；（2）左子结点；（3）右子节点。新插入节点初始颜色为红色。

3. 平衡红黑树：

    > 若插入节点的父节点是黑色，不需要进行修正。如果是红色，则需要进行修正。
   
    插入节点的父节点是祖父节点的左子节点还是右子节点，两种情况对称，以左子结点为例：
   
    `case1` 叔父结点是红色
    - 将父节点和叔父节点染为黑色。

    - 将祖父节点染为红色。

    - 将 `z` 移动到祖父节点位置，继续循环判断。
    
    `case2` 叔父节点是黑色
    - `z` 是右子节点：将 `z` 的父节点左旋，使 `z` 成为左子节点。
    
    - 将父节点染为黑色，祖父节点染为红色，然后对祖父节点右旋，平衡红黑树。

   最后，将根节点染为黑色，确保红黑树的根节点始终为黑色。

**删除节点**







## b/b+树


## hash

## bloom过滤器

# 网络编程

## io复用

### 阻塞和非阻塞

### 水平触发

如果事件和数据已经在缓冲区里，程序调用select()时会报告事件，数据也不会丢失；

如果select()已经报告了事件，但是程序没有处理它，下次调用select()的时候会重新报告。

### 事件

- 可读：1)新客户端的连接请求accept；2)客户端有报文到达recv，可以读；3)客户端连接已断开；

> TCP有缓冲区，如果缓冲区已满，send函数会阻塞
>
> 如果发送端关闭了socket，缓冲区的数据会继续发送给接收端。

- 可写：4)可以向客户端发送报文send，可以写。

> 如果tcp缓冲区没有满，那么socket连接是可写的。
>
> tcp发送缓冲区2.5M，接收缓冲区1M。
>
> 在高并发和流媒体传输场景中，缓冲区有填满的可能。

### select

[code](https://github.com/cyyuz/Cpp/blob/main/src/Linux%E6%9C%8D%E5%8A%A1%E5%99%A8/02.%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/io%E5%A4%8D%E7%94%A8/select.cpp)

```
```



select：等待事件的发生（监视哪些socket发生了事件）。

select用位图（bitmap）表示socket的集合，

- 缺点

> 支持连接数太小(1024)，调整的意义不大，因为连接越多性能越差。
>
> select()是内核函数，每次调用都要把fdset从用户态拷贝到内核态，调用select()之后，把fdset从内核态拷贝到用户态。
>
> select()返回后，需要遍历bitmap，效率比较低。虽然bitmap比较小，但拷贝次数多。

### poll

[code](https://github.com/cyyuz/Cpp/blob/main/src/Linux%E6%9C%8D%E5%8A%A1%E5%99%A8/02.%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/io%E5%A4%8D%E7%94%A8/poll.cpp)

poll模型：可以管理更多的客户端连接，但是连接越多，性能线性下降。

### epoll

[code](https://github.com/cyyuz/Cpp/blob/main/src/Linux%E6%9C%8D%E5%8A%A1%E5%99%A8/02.%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/io%E5%A4%8D%E7%94%A8/poll.cpp)

```
// 创建句柄
int epoll_create(int size);   

// 注册事件
int epoll_ctl(int epfd,int op,int fd,struct epoll_event *event);

// 等待事件
int epoll_wait(int epfd,struct epoll_event *events,int maxevents,int timeout);

struct epoll_event{
    uint32_t events;
    epoll_data_t data;
};
```

epoll没有内存拷贝，没有轮询，没有遍历。

- epoll：只要内存够，管理连接数没有上限，性能不会下降。