---
title: git-remote-to-local
date: 2021-06-22 18:35:55
categories: git
tags: git
---

Git拉取远程仓库的某一分支到本地

a) 本地有其他分支到项目：
git checkout -b localfast origin/fast
git pull origin fast
b)本地没有项目
git clone -b 分支名 仓库地址