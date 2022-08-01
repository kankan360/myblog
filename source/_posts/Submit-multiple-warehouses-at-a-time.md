---
title: git添加多个远程仓库
date: 2019-02-01 10:08:13
categories: "git"
tags: "git"
---

git添加多个远程仓库

配置远程仓库
```
git remote add origin https://url
```
添加另外一个远程仓库
```
git remote set-url --add origin https://url
```
一次性提交到所有仓库
```
git push --all
```
