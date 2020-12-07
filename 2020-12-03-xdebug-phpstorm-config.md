---
title: Linux 下xdebug-phpstorm 安装踩坑记录
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
<!--more-->

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

# 3. 解决`Linux`下xdebug 更新到3.0 `phpstorm` debug 不起作用
## 3.1 原因
* 由于使用`archlinux` 环境, xdebug 版本更新到3.0
* xdebug 将默认的监听口改为了 <font style="font-size:20px; color:red;">9003</font> 而**不是9000**
 ![xdebug03](https://oss.ghovos.top/hexo/myblog/xdebug/xdebug03.png)

## 3.2 将debug端口改为9003
 ![xdebug01](https://oss.ghovos.top/hexo/myblog/xdebug/xdebug01.png)
 ![xdebug02](https://oss.ghovos.top/hexo/myblog/xdebug/xdebug02.png)

* 参考链接:
  * [stackoverflow](https://stackoverflow.com/questions/65092543/how-can-i-connect-xdebug-3-to-phpstorm-on-windows-10)
  * [xdebug.org](https://xdebug.org/docs/upgrade_guide#Step-Debugging)


