---
layout: post
title: HomeBrew的简单使用
date: 2018-07-31
tag: HomeBrew
---

1.基本操作
```bash
$ brew --version 或者 brew -v ：显示HomeBrew 版本信息
$ brew doctor ：检查HomeBrew 的潜在问题
$ brew commands ：查看HomeBrew 的命令
$ brew config ：查看HomeBrew 的全局配置
```

2.搜索软件
```bash
$ brew search <formula> ：搜索需要安装的软件
$ brew search redis ：查询HomeBrew 是否有redis
$ brew search /preg/ ：查询HomeBrew 按照正则查询

$ brew info <formula> ：显示指定软件信息
```

3.查看安装过什么软件
```bash
$ brew list ：查看所有安装包括依赖安装
$ brew leaves ：查看所有安装不包括依赖安装
```

4.安装卸载软件
```bash
$ brow install <formula> ：安装指定软件
$ brow install redis ：安装redis

$ brew reinstall <formula> ：重新安装软件
$ brew reinstall redis ：重新安装redis
$ brew reinstall <formula> --build-from-source :通过源码安装，可以指定一些操作。

$ brew uninstall <formula> 卸载指定软件
$ brew uninstall redis ：卸载redis
$ brew unistall <fromula> --force ：彻底卸载指定软件，包括旧版本
$ brew unistall redis --force ：彻底卸载redis
```

5.安装的软件更新
```bash
$ brew update ：更新HomeBrew 本身的软件的

$ brew upgrade ：更新所有已过时的软件，即列出的已过时软件
$ brew upgrade --all ：更新所有软件，包括未清理干净的旧版本的包
$ brew upgrade <formula> ：更新指定的软件
$ brew upgrade redis ：更新redis

$ brew outdated ：检测已经过时的软件

$ brew pin <formula> ：禁止指定软件更新
$ brew pin redis ：禁止redis更新
$ brew unpin <formula> ：解锁禁止指定软件更新
$ brew unpin redis ：解锁禁止redis更新
```

6.HomeBrew的远程仓库
```bash
$ brew tap ：列出本地资源仓库，其中HomeBrew 是默认仓库，其它都是第三方仓库
$ brew tap <user/repo> 添加第三方仓库，命名的规则按照Github来定的
$ brew untap <user/repo> 删除仓库
```

7.查看指定软件的依赖关系
```bash
$ brew deps <formula> ：查看指定软件依赖于哪些软件
$ brew deps redis ：查看redis软件的依赖关系

$ brew uses <formula> ：查看指定软件被哪些软件所依赖
$ brew uses redis ：查看redis软件的被依赖关系
```

8.清理HomeBrew
```bash
$ brew cleanup 清理所有的过时软件
$ brew cleanup -n ：列出需要清理的内容
$ brew cleanup <formula> ：清理指定的软件过时软件
$ brew cleanup redis ：清理指redis过时软件
```

9.创建、编辑软件脚本信息
```bash
$ brew create [URL [--no-fetch]] ：创建软件包

$ brew edit <formula> ：编辑指定软件脚本信息
$ brew edit redis ：编辑redis脚本信息
```

10.HomeBrew services管理后台服务
```bash
$ brew services ：安装
$ brew services list ：查看服务软件以及运行状态
$ brew services run <formula>|--all ：启动服务，不注册
$ brew services start <formula>|--all ：启动服务，注册
$ brew services stop <formula>|--all ：停止服务，并取消注册
$ brew services restart <formula>|--all ：重启服务，并注册
$ brew services cleanup ：清除已卸载应用的无用的配置

$ brew services start mysql ：开启mysql
$ brew services stop mysql ：停止mysql
$ brew services restart mysql ：重启mysql
```

11.HomeBrew安装图形化软件
```bash
$ brew cask search text 搜索软件
$ brew cask list 列出所有通过cask安装的软件
$ brew cask install <formula> ：安装指定图形界面软件
$ brew cask uninstall <formula> ：卸载指定图形界面软件
$ brew cask uninstall --force <formula> 卸载软件，带参数
```

整理自：[官方文档《Homebrew Documentation》][docs]{:target="_blank"}。  

[docs]: https://docs.brew.sh/Formula-Cookbook.html