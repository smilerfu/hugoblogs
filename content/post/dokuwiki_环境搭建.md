---
title: "DokuWiki环境搭建"
date: 2018-04-05T09:39:00+08:00
lastmod: 2018-04-05T09:39:00+08:00
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

##### CentOS 6.6 x64环境下搭建

1. 下载dokuwiki压缩包: [dokuwiki-c5525093cf2c4f47e2e5d2439fe13964.tgz](https://download.dokuwiki.org/)

2. 切换到目录:

    ```cd /var/www/html```

3. 解压 dokuwiki-c5525093cf2c4f47e2e5d2439fe13964.tgz

    ```tar -zxvf dokuwiki-c5525093cf2c4f47e2e5d2439fe13964.tgz```

    解压完毕后，```在/var/www/html``` 下会出现 ```dokuwiki``` 目录

4. 更改Apache根路径

    ```chown -R apache:root /var/www/html/dokuwiki```

5. 更改目录访问权限

    ```
    chmod -R 664 /var/www/html/dowuwiki
    find /var/www/html/dokuwiki/ -type d -exec chmod 775 {} \;
    ```

6. 安装php，不然打开.php网页时，只会显示php代码，而不是网页页面

    ```yum install php```

7. 启动apache

    ```service httpd start```

8. 访问http://127.0.0.1/dokuwiki/doku.php

    ![](/images/dokuwiki/dokuwiki_install_1.png)

9. 局域网通过IP进行访问需先关闭防火墙

    ```service iptables stop```

    此时可通过http://192.168.x.x/dokuwiki/doku.php进行访问

10. 访问[http://127.0.0.1/dokuwiki/install.php](http://127.0.0.1/dokuwiki/install.php)可进行权限号账号、密码等设置
    ![](/images/dokuwiki/dokuwiki_install_2.png)


11. install.php配置完毕后的界面如下:

   ![](/images/dokuwiki/dokuwiki_install_3.png)

   如果没有出现上界面，而是和第(9)步骤未配置前一样，说明有信息未填写。配置没有生效。

**注意:设置完之后一般将此install.php文件删除，避免遭他人修改**


【附录】

官网: https://www.dokuwiki.org/dokuwiki

下载地址: https://download.dokuwiki.org/



#### 官网插件下载地址

  * 下载地址:https://www.dokuwiki.org/plugins

##### 1.Wrap Plugin 插件

1.下载地址: https://www.dokuwiki.org/plugin:wrap

2.下载后得到 ```dokuwiki_plugin_wrap-stable.zip``` 文件

3.将其解压到 ```/var/www/html/dokuwiki/lib/plugins``` 底下

4.将文件夹名 ```dokuwiki_plugin_wrap-stable``` 重命名为 ```warp```

5.有需要的话重启下网络服务

```
service network restart
```