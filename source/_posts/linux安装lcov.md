---
title: linux安装lcov指定版本
date: 2024-08-02 13:48:40
tags: [linux, lcov]
categories:
- [技术, linux]
---

1. 下载源码 

下载地址：[https://github.com/linux-test-project/lcov/releases](https://github.com/linux-test-project/lcov/releases)，下载指定版本源码到服务器。

![alt text](../img/linux安装lcov/lcov_source_code.png)

2. 解压压缩包

```shell
tar zxvf lcov-1.14.tar.gz
```

3. 编译源码

```shell
cd lcov-1.14/
sudo make install
```

4. 创建链接

lcov默认在 `/usr/local/bin/lcov` ，链接到 `/usr/bin` 目录下。

```shell
sudo ln -s /usr/local/bin/lcov /usr/bin/lcov
```

5. 验证安装

```shell
lcov --version
```
