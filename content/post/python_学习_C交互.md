---
title: "Python学习-Python扩展"
date: 2018-04-05T01:39:00+08:00
lastmod: 2018-04-05T01:39:00+08:00
keywords: []
description: ""
tags: ["Python"]
categories: ["Python"]
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
【注】: 以下环境采用Python3.6.2版本

### 初始化Python虚拟机
```
#include "stdafx.h"
#include <Python.h>
int main()
{
	// 初始化Python解释器
	Py_Initialize();
	if (!Py_IsInitialized())
	{
		PyErr_Print();
		system("pause");
		exit(-1);
	}

	// 将字符串作为代码执行，类似exec
	PyRun_SimpleString("import sys");
	PyRun_SimpleString("print(dir(sys))");

	// 报错堆栈打印
	PyErr_Print();

	// 结束Python解释器
	Py_Finalize();
}
```

### 几个常用接口

##### 1.int PyRun_SimpleString(const char *command) 
将字符串作为代码执行，类似```exec```

返回值: 执行成功返回0，如果有异常返回-1

```
PyRun_SimpleString("import sys");
PyRun_SimpleString("print(dir(sys))");
```

##### 2. PyObject* PyImport_ImportModule(const char *name)
导入一个模块，类似```import```

返回值: PyObject(Return value: New reference)

```
PyObject* mainModule = PyImport_ImportModule("main");
if (!mainModule)
{
	PyErr_Print();
}
```

##### 3. PyObject* PyModule_GetDict(PyObject *module)
获取模块属性字典

PyObject(Return value: Borrowed reference)
```
PyObject* mainDict = PyModule_GetDict(mainModule);
if (!mainDict)
{
	PyErr_Print();
}
```

##### 4. PyObject* PyDict_GetItemString(PyObject *p, const char *key) 
获取模块属性

返回值: PyObject(Return value: Borrowed reference)
```
PyObject* mainStartFunc = PyDict_GetItemString(mainDict, "Start");
if (!mainStartFunc || !PyCallable_Check(mainStartFunc))
{
	PyErr_Print();
}
```

##### 5. PyObject* PyObject_CallFunction(PyObject *callable, const char *format, ...) 
调用一个函数

返回值: PyObject(Return value: New reference)
```
PyObject* returnValue = PyObject_CallFunction(mainStartFunc, NULL);
```

##### 6. void Py_DECREF(PyObject *o) 和 void Py_XDECREF(PyObject *o) 
减引用计数

两个函数区别是:

  - Py_DECREF传入参数o不能为NULL
  - Py_XDECREF允许o为NULL

```
Py_DECREF(returnValue);  // 或者: Py_XDECREF(returnValue); 
```

### New reference 和 Borrowed reference
New reference 会增加引用计数，因此在释放时需要调用```Py_DECREF```或者```Py_XDECREF```进行减引用计数