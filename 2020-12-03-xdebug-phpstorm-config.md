---
title: LINUX 下xdebug-phpstorm 安装踩坑记录
mathjax: true
tags:
  - xdebug
  - phpstorm
categories:
  - 常用笔记
date: 2020-12-03 16:00:36
---

# 1. 安装xdebug
```sh
sudo pacman -S xdebug
# apt / yum 类似
```


# 2. 编辑xdebug.ini文件
```sh
sudo vim  /etc/php/conf.d/xdebug.ini
```

```ini
zend_extension=xdebug.so
; xdebug 3 的特性
xdebug.mode = debug
xdebug.idekey = PHPSTORM   
xdebug.show_error_trace = 1
xdebug.remote_autostart = 0 
xdebug.remote_handler = dbgp
xdebug.remote_mode = "req"
xdebug.remote_log=/tmp/xdebug.log
```

# 3. 解决`Linux`下xdebug 更新到3.0 `phpstorm` 不起作用
```

```

# 

* 由于使用`archlinux` 环境开发，软件包比较新
* xdebug 版本更新到3.0

