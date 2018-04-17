---
title: "Lua 学习笔记"
date: 2018-04-15T01:39:00+08:00
lastmod: 2018-04-15T01:39:00+08:00
keywords: []
description: ""
tags: []
categories: ["Lua"]
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


##### 8个基本类型
lua有8个基本类型，分别为: nil、boolean、number、string、userdata、function、thread、table
可使用type函数获取变量的类型，返回一个字符串:
```print(type(123))  -->  number```

##### Booleans
lua除了false和nil为假，其余都为真，0和空字符串也为真。
