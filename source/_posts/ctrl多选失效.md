---
layout: ctrl
title: ctrl多选失效
date: 2017-07-04 23:35:24
tags: vmware
---

## 解决MacOSX下的VMWare中Ubuntu按ctrl不能多选文件的问题

在VMWare中，虚拟机 -> 设置 -> 键盘与鼠标 -> 将默认的配置文件改为Mac的配置文件。

注意：这个方法可以解决ctrl不能实现多选的问题，但是会使得Mac的快捷键在虚拟机中失效，例如command+c在虚拟机中不能再复制，需要使用ctrl+c。