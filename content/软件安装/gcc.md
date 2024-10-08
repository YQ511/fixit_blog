---
title: Gcc
subtitle:
date: 2024-03-26T16:47:43+08:00
draft: false
type: posts
author:
  name:
  link:
  email:
  avatar:
description:
keywords:
license:
comment: false
weight: 0
tags:
  - 软件安装
categories:
  - 软件安装
hiddenFromHomePage: false
hiddenFromSearch: false
summary:
resources:
  - name: featured-image
    src: featured-image.jpg
  - name: featured-image-preview
    src: featured-image-preview.jpg
toc: true
math: false
lightgallery: false
password:
message:
repost:
  enable: true
  url:

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---
### [GCC所需依赖](https://blog.csdn.net/nie19940803/article/details/102408025)
[isl](https://blog.csdn.net/m0_62342492/article/details/136540454)参考
```sh
wget ftp://ftp.gnu.org/gnu/mpc/mpc-1.0.2.tar.gz
wget ftp://ftp.gnu.org/gnu/gmp/gmp-5.0.1.tar.bz2
wget http://ftp.gnu.org/gnu/mpfr/mpfr-3.1.2.tar.gz
wget https://libisl.sourceforge.io/isl-0.20.tar.gz
```
### [Makefile简介及如何指定头文件和库文件](https://blog.csdn.net/new9232/article/details/129107708)
vim Makefile
加入INCLUDES = -I/public/home/yuqing/prefix/include 

```sh
#../../gcc/hwint.h:62:5: error: #error "Unable to find a suitable type for HOST_WIDE_INT"
unset LIBRARY_PATH CPATH C_INCLUDE_PATH PKG_CONFIG_PATH CPLUS_INCLUDE_PATH INCLUDE
mkdir build;cd build;
../configure --prefix=/public/home/yuqing/prefix --enable-threads=posix --disable-checking --enable--long-long --enable-languages=c,c++,fortran --disable-multilib  --with-gmp=/public/home/yuqing/prefix --with-mpfr=/public/home/yuqing/prefix --with-mpc=/public/home/yuqing/prefix --with-isl=/public/home/yuqing/prefix
make&&make install
```

### [zstd库的缺失](https://blog.csdn.net/qq_36836950/article/details/135225444)
```sh
wget http://security.ubuntu.com/ubuntu/pool/main/libz/libzstd/libzstd_1.5.5+dfsg2.orig.tar.xz
tar xvf libzstd_1.5.5+dfsg2.orig.tar.xz
mkdir gcc_lib
make lib CC=gcc -j $(grep "cpu cores" /proc/cpuinfo | wc -l) #设置gcc编译器和编译内核数
make install PREFIX=$(pwd)/gcc_lib #设置库安装位置到指定路径
```
报错Error: ../.././gcc/lto-compress.cc:39:18: fatal error: zstd.h: No such file or directory

### [/usr/bin/ld: cannot find -lxxx 的解决办法](https://blog.csdn.net/zaf0516/article/details/108979759)

### [perl的安装](https://www.jianshu.com/p/43cbbb16575c)

### [rpm包的解压缩]()
```sh
rpm2cpio *.rpm | cpio -idvm
```
