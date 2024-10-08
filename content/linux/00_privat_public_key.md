---
title: 设置ssh通过秘钥登录
subtitle:
date: 2023-10-11T10:24:59+08:00
draft: false
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
  - linux
categories:
  - linux
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

<!--more-->
# 秘钥登录[帖子](https://www.cnblogs.com/narrnhu/p/17538147.html#:~:text=%E5%BD%93%E4%BD%A0%E5%AE%8C%E6%88%90%E5%85%A8%E9%83%A8%E8%AE%BE%E7%BD%AE%EF%BC%8C%E5%B9%B6%E4%BB%A5%E5%AF%86%E9%92%A5%E6%96%B9%E5%BC%8F%E7%99%BB%E5%BD%95%E6%88%90%E5%8A%9F%E5%90%8E%EF%BC%8C%E5%86%8D%E7%A6%81%E7%94%A8%E5%AF%86%E7%A0%81%E7%99%BB%E5%BD%95%EF%BC%9A%20PasswordAuthentication%20no%20%E6%9C%80%E5%90%8E%EF%BC%8C%E9%87%8D%E5%90%AF%20SSH,%E6%9C%8D%E5%8A%A1%EF%BC%9A%20%5Broot%40host.ssh%5D%24%20service%20sshd%20restart)
1. 密码登录到你打算使用密钥登录的账户
```
ssh-keygen #建立秘钥对
``` 
弹出提示符
```
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): <== 按 Enter
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase): <== 输入密钥锁码，或直接按 Enter 留空
Enter same passphrase again: <== 再输入一遍密钥锁码
Your identification has been saved in /root/.ssh/id_rsa. <== 私钥
Your public key has been saved in /root/.ssh/id_rsa.pub. <== 公钥
The key fingerprint is:
0f:d3:e7:1a:1c:bd:5c:03:f1:19:f1:22:df:9b:cc:08 root@host
```
2. 公钥的安装以及文件权限赋予
```
cd .ssh ; cat id_rsa.pub >> authorized_keys ; chmod 600 authorized_keys ; chmod 700 ~/.ssh
```
3.  秘钥密码的设置
```
ssh-keygen -p -f ~/.ssh/id_rsa
```
设置 SSH，打开密钥登录功能
```
vim /etc/ssh/sshd_config
#######################################
PubkeyAuthentication yes
RSAAuthentication yes #如果没有无需设置
PermitRootLogin yes #root用户能否通过SSH登录
PasswordAuthentication no #禁用密码登录
######################################
#service sshd restart 
systemctl restart sshd.service #重启 SSH 服务
```
分发秘钥，通过xshell等客户端载入秘钥
