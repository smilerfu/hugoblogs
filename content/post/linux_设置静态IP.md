---
title: "Linux 设置静态IP"
date: 2018-04-05T01:39:00+08:00
lastmod: 2018-04-05T01:39:00+08:00
keywords: []
description: ""
tags: ["Linux"]
categories: ["Linux"]
author: ""

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: true
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
---

<!--more-->
【注】: 以下环境在CentOS系统上

网络配置的配置文件在```/etc/sysconfig/network-scripts/```下，文件名前缀为```ifcfg-```后面跟的就是网卡的名称，可以通过双TAB键查看然后编辑。

例如网卡名为 eth0 的配置文件为: ```ifcfg-eth0```

```ifcfg-lo```是本地回环地址的配置文件，所有计算机都有，无需修改。

默认情况下，是DHCP动态获取的。配置文件内容如下:
![](/images/linux/static_ip/linux_static_ip_1.png)

如果需要改成静态的，修改的地方如下:

1. 把 ```BOOTPROTO=dhcp``` 改成 ```BOOTPROTO=static``` 表示静态获取

2. 在最后追加下面的配置：
    ```
    BROADCAST=192.168.1.255
    IPADDR=192.168.1.123
    NETMASK=255.255.255.0
    GATEWAY=192.168.1.1
    ```
    设置说明:\\
    - BROADCAST - 局域网广播地址
    - IPADDR - 静态IP
    - NETMASK - 子网掩码
    - GATEWAY - 网关或者路由地址

    需要说明，原来还有个NETWORK配置的是局域网网络号，这个是ifcalc自动计算的，所以这里配置这些就足够了

    配置如下图:
    ![](/images/linux/static_ip/linux_static_ip_2.png)

3. 这时候重启下网络服务器

    使用命令行:```service network restart```或者```/etc/init.d/network restart```

4. 重启后，静态ip就生效了

5. 发现无法连接外网

    配置成功后，dns配置一般会消失，所以这时候就ping不通域名了，无法连接外网，需要配置DNS，配置文件位置是：```/etc/resolv.conf```，里面的nameserver指定dns服务器地址。

    但是我们修改的文件仍然是```ifcfg-eth0```

    使用命令<code shell> ipconfig /all </code>查看主机(Windos)的DNS配置如下:
    ![](/images/linux/static_ip/linux_static_ip_5.png)

    在配置文件末尾增加如下配置:
    ```
    DNS1=114.114.114.114
    DNS2=100.63.0.1
    DNS3=202.96.128.166
    ```

    ![](/images/linux/static_ip/linux_static_ip_3.png)

    然后和步骤3一样，重启下网络服务器

    此时再去重新看```resolv.conf```文件内容，发现此文件已经更新。

    ![](/images/linux/static_ip/linux_static_ip_4.png)


