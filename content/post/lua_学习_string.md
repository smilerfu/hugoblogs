---
title: "Lua string"
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
##### 参考文档
[http://www.lua.org/manual/5.3/manual.html#pdf-string Manipulation](http://www.lua.org/manual/5.3/manual.html#pdf-string Manipulation)


##### string.byte (s [, i [, j]])

```
-- 功能: 返回字符 s[i], s[i+1], ..., s[j]的数字码。
-- 参数: 默认值: i=1, j=i.
-- 返回值: 返回数字码串
print(string.byte("acb", 1,3))  --> 97	99	98
```

##### string.char (···)
```
-- 功能: 将number的数字码转为字符
-- 参数: number
-- 返回值: 返回字符串

print(string.char(97, 99, 98))  --> acb
```

##### string.dump (function [, strip])
```
-- 功能: 将一个函数序列化，返回序列化后的二进制字符串。之后可以使用load加载这个字符串。
-- 参数: strip如果为true，序列化后的字符串将不会包含任何debug信息，可以节省空间。
-- 返回值: 返回序列化后的二进制字符串

-- 普通函数
function dumpTest(v)
    print("dumpTest: " .. v)
end

dumpString = string.dump(dumpTest)
loadFunc = load(dumpString)
loadFunc("abcd")  -> dumpTest: abcd

-- 闭包函数
function dumpTestClosure()
    i = 0
    local  function innerFunc()
    i = i + 1
    print("inner: " .. i)
    end
    return innerFunc
end

closureFunc = dumpTestClosure()
closureFunc()  --> inner: 1
closureFunc()  --> inner: 2
dumpString = string.dump(closureFunc,true)
loadFunc = load(dumpString)
loadFunc()  --> inner: 3
```

##### string.find (s, pattern [, init [, plain]])
```
-- 功能: 查找字符串s中第一个符合pattern的位置
-- 参数: init 搜索的起始位置，默认 init=1(可以为负数，表示从后往前数的字符个数)
--       plain 默认 plain=false，如果为true表示关闭模式匹配，只做简单的查找子串的操作。
-- 返回值: 找到返回起始位置和终止位置，没找到返回nil
print(string.find("abcdabcdabcd", "cda"))  --> 3	5
print(string.find("abcdabcdabcd", "d"))  --> 4	4
print(string.find("abcdabcdabcd", "123"))  --> nil

print(string.find("abcdabcdabcd", "cda", 4))  --> 7	9
print(string.find("abcdabcdabcd", "cda", -9))  --> 7	9
print(string.find("abcdabcdabcd", "cda", -11))  --> 3	5
```


##### gsub
```
print(string.gsub("one string", "one", "another"))
```
