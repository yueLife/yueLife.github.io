---
layout: post
title: Git skills
date: 2017-06-02
tag: git 
---

1.  **修改.gitignore后生效**  

    在使用git的时候我们有时候需要忽略一些文件或者文件夹。我们一般在仓库的根目录创建.gitignore文件。  
    在提交之前，修改.gitignore文件，添加需要忽略的文件。然后再做`add` `commit` `push`等。  
    但是有时在使用过称中，需要对.gitignore文件进行再次的修改。这次我们需要清除一下缓存cache，才能使.gitignore生效。  
    例：
```bash
$ git rm -r --cached .  #清除缓存  
$ git add . #重新trace file  
$ git commit -m "update .gitignore" #提交和注释  
$ git push origin master #可选，如果需要同步到remote上的话
```
    这样就能够使修改后的.gitignore生效。   

2.  **获取git项目最后的tag**  
    `git describe` 命令显示离当前提交最近的标签。  
    使用语法：
```bash
$ git describe [--all] [--tags] [--contains] [--abbrev=<n>] [<commit-ish>…​]
$ git describe [--all] [--tags] [--contains] [--abbrev=<n>] --dirty[=<mark>]
```
    例：
```bash
$ git tag -n10  
        v1.0.0          create v1.0.0 tag
        v1.0.1          create v1.0.1 tag
        v1.1.0          create v1.1.0 tag
        v1.1.1          create v1.1.1 tag
$ git describe --tags `git rev-list --tags --max-count=1` # 显示最新的一个tag v.1.1.1
```

