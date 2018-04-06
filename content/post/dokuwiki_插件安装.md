---
title: "DokuWiki插件安装"
date: 2018-04-05T01:39:00+08:00
lastmod: 2018-04-05T01:39:00+08:00
keywords: []
description: ""
tags: []
categories: [DokuWiki]
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

#### 官网插件下载地址

  * 下载地址:https://www.dokuwiki.org/plugins

##### Wrap Plugin 插件

1.下载地址: https://www.dokuwiki.org/plugin:wrap

2.下载后得到 ```dokuwiki_plugin_wrap-stable.zip``` 文件

3.将其解压到 ```/var/www/html/dokuwiki/lib/plugins``` 底下

4.将文件夹名 ```dokuwiki_plugin_wrap-stable``` 重命名为 ```warp```

5.有需要的话重启下网络服务

```
service network restart
```