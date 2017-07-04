---
layout:     post
title:      "深入理解计算机系统"
subtitle:   "deeply learn computer system"
date:       2017-07-04
author:     "NL"
header-img: "img/post-bg-2015.jpg"
tags:
- computer_system
---


## 深入理解计算机系统 第二章

1. long int、char * 在32位的机器中字节数为4位，而在64位的机器中是8位。
2. $a \& (b or c)=(a\&b) or (a\&b)​$
3. C\C++支持**有符号或无符号数**，Java只支持**有符号数**。
4. 负数在计算机中的存储是采用**二进制补码**的形式。 
5. 有符号值使用**算术移位**，无符号数使用**逻辑移位**


## 第三章

1. 数据对齐：**short**为2的倍数，**int, int *, float, double**为4的倍数。**栈帧中以每个块**必须为16字节对齐的倍数。

