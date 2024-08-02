---
title: linux安装cmake指定版本
date: 2024-08-02 15:14:04
tags: [linux, cmake]
categories:
- [技术, linux]
---

1. 下载源码 

下载地址：[https://github.com/Kitware/CMake/releases](https://github.com/Kitware/CMake/releases)，下载指定版本源码到服务器。

![alt text](../img/linux安装cmake指定版本/cmake.png)

2. 解压压缩包

```shell
tar zxvf CMake-3.28.4.tar.gz
```

3. 编译源码

```shell
cd CMake-3.28.4/
./bootstrap
make
sudo make install
```

4. 验证安装

```shell
cmake --version
```
