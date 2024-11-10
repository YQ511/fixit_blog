---
title: Git
subtitle:
date: 2024-08-28T10:19:40+08:00
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
  - Github-git
categories:
  - Github-git
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

## [git学习](https://zhuanlan.zhihu.com/p/404642045)

```sh
#C:\Users\90500\.ssh
#https://github.com/YQ511/insermind.git
#git remote add origin https://github.com/YQ511/fixit_blog.git
#origin: https://github.com/YQ511/insermind.git
#git pull origin main --allow-unrelated-histories
#git branch -m master main
function updateRemote (){
        git add .  #from working directory to staging area/index
        git commit -m "test" #from staging area/index to local repository
        git push origin main
}
updateRemote
function updateLocal(){
git checkout mian #switch to the branch or recover the files
git fetch origin
git pull origin main
}
#updateLocal
```

<div style="text-align: center;">
  <img src="/gitLearn.png" width="9999" height="19692">
</div>