---
layout: post
title: Git 清理提交记录
date: 2020-07-15
tag: Git 
---

有时候git 的提交的日志过多，需要删除下所有历史提交记录，只留下最新的干净代码。

新建仓库，并增加几条提交记录：
```bash
$ git lg -n 5
* def4f33 - (HEAD -> master) 5.txt (2020-07-15 13:11:53)
* dbc5e1e - 4.txt (2020-07-15 13:11:32)
* 045ee8c - 3.txt (2020-07-15 13:11:20)
* 6026d34 - 2.txt (2020-07-15 13:10:53)
* a843772 - 1.txt (2020-07-15 13:10:27)

$ git branch
* master
```

一般删除.git文件夹，然后强制提交远程仓库。
```bash
$ rm -rf .git # 删除.git

$ git init # 初始化git 仓库
Initialized empty Git repository in ****/.git/

 # 添加远程仓库地址
$ git remote add origin git@github.com:***/***.git

# 添加所有文件，并提交
$ git add -A
$ git commit -m '1.仓库初始化，添加文件'

 # 强制提交，因为远程仓库有数据
$ git push -fu origin master
```

第二种是新建分支，删除master分支，最后强制提交远程仓库
```bash
$ git checkout --orphan new_branch  # 创建一个新的初始分支，无文件提交
Switched to a new branch 'new_branch'

# 添加所有文件，并提交
$ git add -A 
$ git commit -m '1.仓库初始化，添加文件'
$ git branch
  master
* new_branch

# 删除master 分支
$ git branch -D master 
Deleted branch master (was def4f33).
$ git branch
* new_branch

# 重命名new_branch 为master 分支
$ git branch -m master 
$ git branch
* master

# 只有一条刚刚操作的记录
$ git lg -n 5
* 9afa63b - (HEAD -> master) 1.仓库初始化，添加文件 (2020-07-15 13:15:27)

 # 强制提交，因为远程仓库有数据
$ git push -f origin master
```