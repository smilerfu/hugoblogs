---
title: "C++ 学习笔记"
date: 2018-04-16T01:39:00+08:00
lastmod: 2018-04-16T01:39:00+08:00
keywords: []
description: ""
tags: []
categories: ["C", "C++"]
author: ""

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
---

<!--more-->

##### 前置(后置)递增(递减)运算符
  - 前置递增:```++i``` 等价于 ```i=i+1, i```
  - 后置递增:```i++``` 等价于 ```temp=i, i=i+1, temp```

    temp是编译器产生的一个临时变量，只能作为右值使用。

##### 左值和右值
  - ```++i```是左值(可以形象地记为++在i左边)
  - ```i++```是右值(可以形象地记为++在i右边)

左值是可以写在等号左边的表达式，必须是一个非const的变量。\\
右值是可以写在等号右边的表达式，可以是一个常量,一个字面数字，或者说一个任意的可以求值的表达式。\\
一个可以作为左值的表达式,同时也是可以作为右值使用的。\\
如果对右值进行了左值的操作，那么是错误的。

例如:

###### 效率
  - ```++i```效率更高效一些，因为```i++```产生了一个临时的变量temp

###### 测试代码
```c++
#include <iostream>  
using namespace std;  
  
int main()  
{  
    int i=0;  
    ++++i; // All Right  
    //i++++; // error C2105: '++' needs l-value  
    //++i=10; // All Right  
    //i++=10; // error C2106: '=' : left operand must be l-value  
    //++i++; // error C2105: '++' needs l-value  
    return 0;  
}  
```