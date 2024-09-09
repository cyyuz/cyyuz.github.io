---
title: ls
date: 2024-08-31 16:38:24
tags:
---

# 数据结构

## 红黑树

[code](https://github.com/cyyuz/code-demos/blob/main/src/linux-server/01.%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84/%E7%BA%A2%E9%BB%91%E6%A0%91/rbtree.cpp)

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

## b/b+树


## hash

## bloom过滤器

# 网络编程

## socket

[code](https://github.com/cyyuz/code-demos/blob/main/src/linux-server/02.%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/io_multiplexing/socket_server1.cpp)

```c++
/**
 * @brief 创建 socket 文件描述符
 * @param domain 套接字族，AF_INET (IPv4) 或 AF_INET6 (IPv6)
 * @param type 套接字类型，SOCK_STREAM (TCP) 或 SOCK_DGRAM (UDP)
 * @param protocol 协议，通常为 0
 * @return 返回 socket 文件描述符，-1 表示出错
 */
int socket(int domain, int type, int protocol);

/**
 * @brief 绑定 socket 到指定的 IP 地址和端口号
 * @param socket socket 文件描述符
 * @param address 指向 sockaddr 结构体的指针，包含 IP 地址和端口号
 * @param address_len sockaddr 结构体的大小
 * @return 成功返回 0，失败返回 -1
 */
int bind(int socket, const struct sockaddr *address, socklen_t address_len);

/**
 * @brief 监听 socket，准备接受连接
 * @param socket socket 文件描述符
 * @param backlog 连接队列的最大长度
 * @return 成功返回 0，失败返回 -1
 */
int listen(int socket, int backlog);

/**
 * @brief 接受连接
 * @param socket socket 文件描述符
 * @param address 指向 sockaddr 结构体的指针，用于存储连接客户端的 IP 地址和端口号
 * @param address_len 指向 socklen_t 类型的指针，用于存储 sockaddr 结构体的大小
 * @return 返回新的 socket 文件描述符，失败返回 -1
 */
int accept(int socket, struct sockaddr *address, socklen_t *address_len);

/**
 * @brief 连接到服务器
 * @param socket socket 文件描述符
 * @param address 指向 sockaddr 结构体的指针，包含服务器的 IP 地址和端口号
 * @param address_len sockaddr 结构体的大小
 * @return 成功返回 0，失败返回 -1
 */
int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen);

/**
 * @brief 发送数据
 * @param socket socket 文件描述符
 * @param buffer 指向要发送的数据的指针
 * @param length 要发送的数据的长度
 * @param flags 发送标志，通常为 0
 * @return 返回实际发送的字节数，失败返回 -1
 */
ssize_t send(int socket, const void *buffer, size_t length, int flags);

/**
 * @brief 接收数据
 * @param socket socket 文件描述符
 * @param buffer 指向接收数据的缓冲区的指针
 * @param length 缓冲区的大小
 * @param flags 接收标志，通常为 0
 * @return 返回实际接收到的字节数，失败返回 -1
 */
ssize_t recv(int socket, void *buffer, size_t length, int flags);

/**
 * @brief 关闭 socket
 * @param socket socket 文件描述符
 * @return 成功返回 0，失败返回 -1
 */
int close(int socket);
```

## io复用

### 阻塞和非阻塞

阻塞：当调用一个函数时，当前线程会被挂起，直到函数返回结果。这种模式通常会导致线程在等待的期间无法执行其他操作。

非阻塞：当调用一个函数时，函数立即返回，不会阻塞当前线程。即使操作尚未完成，线程仍然可以继续执行其他任务。非阻塞模式通常需要通过轮询或事件驱动机制来处理操作完成后的结果。

### 事件触发

水平触发： 

如果事件和数据已经在缓冲区里，程序调用select()时会报告事件，数据也不会丢失；

如果select()已经报告了事件，但是程序没有处理它，下次调用select()的时候会重新报告。

边沿触发：

**水平触发（Level-Triggered）**

如果事件和数据已经在缓冲区里，程序调用 select() 时会报告事件，数据也不会丢失；

如果 select() 已经报告了事件，但是程序没有处理它，下次调用 select() 的时候会重新报告。

**边沿触发（Edge-Triggered）**

当事件的状态发生变化时，只报告一次。这意味着如果数据到达并触发了事件，但程序没有立即处理它，那么在数据被读取之前，这个事件不会再次被报告。

### 事件

**可读事件：**

1. 新连接请求accept；

2. 客户端有数据到达，使用 recv() 进行读取。

3. 客户端连接断开。

注意：

> TCP协议有缓冲区。如果缓冲区已满，send() 函数可能会阻塞。
>
> 即使发送端关闭了 socket，缓冲区中的数据也会继续发送到接收端。

**可写事件：**

1. 可以使用 send() 向客户端发送数据。

注意：

> 如果 TCP 缓冲区没有满，那么 socket 连接是可写的。
>
> TCP 发送缓冲区通常为 2.5 MB，接收缓冲区通常为 1 MB。
>
> 在高并发或流媒体传输场景中，缓冲区可能会被填满。

### select

[code](https://github.com/cyyuz/code-demos/blob/main/src/linux-server/02.%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/io_multiplexing/select.cpp)

`select` 是一个用于异步 I/O 多路复用的函数，在网络编程中非常有用。它允许一个进程监视多个文件描述符（通常是套接字），并等待其中一个或多个文件描述符变为可读、可写或出现异常。

```cpp
/**
 * @brief 监视多个文件描述符的读/写事件
 * @param nfds 监视的文件描述符个数
 * @param readfds 监视可读事件的文件描述符集合
 * @param writefds 监视可写事件的文件描述符集合
 * @param exceptfds 监视异常事件的文件描述符集合
 * @param timeout 超时时间
 * @return 返回发生事件的文件描述符个数，0表示超时，-1表示出错
 */
int select(int nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct timeval *timeout);
```

select：等待事件的发生（监视哪些socket发生了事件）。

select用位图（bitmap）表示socket的集合，

**缺点：**

1. 连接数量限制：select 的最大监视文件描述符数目是有限制的，默认是 1024。尽管可以通过修改内核参数来增加这个限制，但更多的连接会导致性能下降。

2. 效率问题：每次调用 select 都需要在用户态和内核态之间复制文件描述符集合。此外，返回后还需要遍历整个位图来查找哪些描述符已就绪。

3. 性能瓶颈：随着监视的文件描述符数量增加，select 的性能会逐渐下降。

### poll

[code](https://github.com/cyyuz/code-demos/blob/main/src/linux-server/02.%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/io_multiplexing/poll.cpp)

可以管理更多的客户端连接，但是连接越多，性能线性下降。

### epoll

[code](https://github.com/cyyuz/code-demos/blob/main/src/linux-server/02.%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/io_multiplexing/epoll.cpp)

```c++
// 创建句柄
int epoll_create(int size);   

// 注册事件
int epoll_ctl(int epfd,int op,int fd,struct epoll_event *event);

// 等待事件
int epoll_wait(int epfd,struct epoll_event *events,int maxevents,int timeout);
```

epoll没有内存拷贝，没有轮询，没有遍历。

- epoll：只要内存够，管理连接数没有上限，性能不会下降。

### reactor

[code](https://github.com/cyyuz/code-demos/blob/main/src/linux-server/02.%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/io_multiplexing/reactor1.cpp)

Reactor 是一种用于处理并发事件的设计模式，通常用于 I/O 多路复用 环境。它通过一个事件循环等待事件的到来，然后分发这些事件给相应的处理程序进行处理。Reactor 模式广泛应用于网络编程和服务器端开发。

- 事件循环（Event Loop）：Reactor 模式的核心是一个循环，负责监听和捕获输入/输出事件。

- 事件分发器（Dispatcher）：一旦事件被捕获，Reactor 将事件分发给相应的处理程序。

- 事件处理程序（Handler）：这是实际处理事件的代码。处理程序与事件关联，通常对应某种 I/O 操作（如读取、写入、连接等）。

Reactor 模式可以在不使用多线程或多进程的情况下高效处理大量的并发连接，特别适合处理大量 I/O 事件的场景，如网络服务器。

业务网络隔离

### 
并发：服务端同时承载的客户端数量
qps  最大时延 新建（建链）  吞吐量





并发多少：

测试结果

线上实际情况