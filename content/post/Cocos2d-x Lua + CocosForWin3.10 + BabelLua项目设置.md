---
title: "Cocos2d-x Lua + CocosForWin3.10 + BabelLua项目设置"
date: 2018-05-13T14:59:45+08:00
lastmod: 2018-05-13T14:59:45+08:00
draft: false
keywords: ["Cocos2dX", "Babelua"]
description: ""
tags: []
categories: ["Cocos2dX", "Babelua"]
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

#### 项目环境
  - cocos2d-x-3.16
  - VS2013
  - CocosForWin-v3.10.exe
  - BabeLua+For+2013+V3.2.2.0.vsix

#### 创建项目
###### 新建Cocos2d-x lua项目
  - 切换到```cocos2d-x-3.16\tools\cocos2d-console\bin```目录，执行:

    ```
    cocos new MyLuaGame -l lua -p com.xxx.xxx -d F:\cocosproject
    ```
  - 编译项目

###### 新建 Cocostudio项目
  - 打开Cocostudio，选择【文件】，选择【新建项目】
  ![](/images/cocos2dx/cocostudio_new_project.png)
  - 将```F:\cocosproject\MyLuaGame\CocosProject\cocosstudio```拷贝到项目根目录，即```F:\cocosproject\MyLuaGame```
  - 将```CocosProject.ccs```、```CocosProject.cfg```和```CocosProject.udf```也拷贝到项目根目录，即```F:\cocosproject\MyLuaGame```
  - 拷贝完毕后，CocosProject这个目录就没有什么用，可以删掉了
  - 修改```CocosProject.cfg```文件中的```CreateFrameworkVersion Value="cocos2d-x-3.16"```和```CurrentFrameworkVersion Value="cocos2d-x-3.16```，目前不清楚此修改是否有作用
  - 使用Cocostudio打开项目，选择```F:\cocosproject\MyLuaGame\CocosProject.ccs```打开即可。

###### 新加 lua项目
  - 右键解决方案，添加并新建Lua项目
  ![](/images/cocos2dx/solution_add_lua_project.png)
  - Lua项目路径设置为项目MyLuaGame的根路径
  ![](/images/cocos2dx/lua_project_new.png)
  - 右键Lua项目，选择添加现有目录，将F:\cocosproject\MyLuaGame\src目录添加入
  ![](/images/cocos2dx/lua_project_add_existing_folder.png)
  - 右键LuaProject，选择属性，设置Lua exe path为```$(SolutionDir)../../simulator/win32/MyLuaGame.exe```和Working path为```$(SolutionDir)../../```
  ![](/images/cocos2dx/lua_project_set_path.png)
  - 设置LuaProject为启动项目
  - 此时添加断点发现并不能中断，修改AppDelegate.cpp文件，添加```LuaStack* stack = engine->getLuaStack();stack->addSearchPath("src/");```
  ![](/images/cocos2dx/lua_project_debug_appdelegate.png)
  - 设置MyLuaGame为启动项目，重新编译运行后，再设置LuaProject为启动项目，此时可以进入断点
  

