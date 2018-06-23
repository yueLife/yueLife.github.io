---
layout: post
title: Composer Some Question
date: 2017-05-17
tag: Composer
---

1.[Composer Update silently returns "Killed"](https://github.com/composer/composer/issues/1815){:target="_blank"}

以前在学习的时候，买的最低配置的云服务器内存只有可怜的0.5G。以至于更新Composer的时候，提示被killed。
```bash
$ composer update
    Loading composer repositories with package information
    Updating dependencies (including require-dev)
    Killed
```
可以把调整swap到1G，这样就可以正常更新Composer了。

```bash
$ /bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=1024
$ /sbin/mkswap /var/swap.1
$ sudo /sbin/swapon /var/swap.1
```

